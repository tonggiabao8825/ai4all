---
layout: post
title: "Một số kỹ thuật Clean Code cho Prompt Template trong Python"
date: 2025-11-20 22:31:00 +0700
author: baro
categories: [ai, machine-learning, clean-code]
tags: [llm, python, rag, prompt-engineering, jinja2]
image: https://miro.medium.com/v2/resize:fit:2000/1*a_jE0zvn4eXUxL6rCsYe2g.png
excerpt: "Tổng hợp đầy đủ các phương pháp xử lý Multi-line String trong Python. Giúp bạn quản lý Prompt cho RAG gọn gàng, logic và dễ bảo trì."
---

## Mở đầu

Chào các bạn, khi làm việc với Generative AI, đặc biệt là xây dựng ứng dụng RAG (Retrieval-Augmented Generation), chiếc **"Prompt"** chính là linh hồn của ứng dụng. Tuy nhiên, khi nhúng những đoạn văn bản dài vào trong code Python (Hardcode), chúng ta thường gặp xung đột giữa **thẩm mỹ của code** (thụt đầu dòng đúng chuẩn) và **định dạng của chuỗi** (không thừa khoảng trắng).

Bài viết này mình sẽ tổng hợp **tất cả các cách** để xử lý vấn đề này, đi từ những mẹo nhỏ nhất cho đến cách tổ chức kiến trúc chuyên nghiệp.
Một ví dụ như sau:



```python
class DeepSeekService:
    def __init__(self):
        # Khởi tạo OpenAI client với Azure config
        self.client = openai.OpenAI(
            api_key=os.getenv("AZURE_API_KEY"),
            base_url="https://DeepSeek-R1-xacdm.eastus.models.ai.azure.com"
        )
        self.model = "deepseek-chat"
    def generate_response(self, prompt: str) -> str:
        try:
            logger.info("Sending request to DeepSeek API")
            messages = [
                {"role": "system", "content": "You are an AI assistant with expertise in AI, Machine Learning, and Software Development. Answer questions based on the provided CV context. DO NOT include any thinking process or notes to yourself in your response. Provide direct, concise answers only."},
                {"role": "user", "content": prompt}
            ]
            response = self.client.chat.completions.create(
                model=self.model,
                messages=messages,
                max_tokens=1000,
                temperature=0.7
            )
            # Lấy response content
            return response.choices[0].message.content

```



Đoạn code trên khai báo một class để sử dụng API của model DeepSeek mình tự finetune và deploy trên AzureCloud. Tất nhiên là bây giờ baseurl không thế dùng được nữa vì mình làm gì còn credit để duy trì đâu :v.

Nhìn vào phần system-prompt ta có thể thấy dài và rất xấu, nhiều khi không focus được vào các rule chính. 
Mình cùng thử xem sau khi áp dụng các cách của bài viết này thì có thay đổi gì nhé!


## Vấn đề: Cuộc chiến giữa Indentation và String

Hãy bắt đầu với ví dụ kinh điển gây đau đầu. Bạn muốn code thụt dòng đẹp, nhưng Python lại hiểu nhầm ý bạn.

```python
def get_system_prompt():
    # Code thụt vào cho đẹp
    prompt = """You are an AI assistant.
    Your task is to analyze the document.
    Be concise."""
    return prompt

print(get_system_prompt())
````

**Kết quả (Xấu):**

```text
You are an AI assistant.
    Your task is to analyze the document.  <-- Bị dính khoảng trắng thừa
    Be concise.                            <-- Bị dính khoảng trắng thừa
```


-----


Dùng cho các prompt ngắn, đơn giản, không có quá nhiều logic phức tạp.



### Cách sử dụng `textwrap.dedent` 

Đây là cách "sạch" nhất nếu bạn vẫn muốn dùng Triple Quotes (`"""`). Thư viện chuẩn `textwrap` sẽ cắt bỏ phần thụt đầu dòng chung.

```python
import textwrap

def get_prompt_v2():
    # Ký tự \ ở dòng đầu để tránh dòng trống đầu tiên
    prompt = textwrap.dedent("""\
        You are an AI assistant.
        Your task is to analyze the document.
        Be concise.
    """)
    return prompt
```

  * **Ưu điểm:** Viết tự nhiên, copy-paste từ file text vào code dễ dàng, không lo về `\n`.
  * **Nhược điểm:** Phải import thêm thư viện (nhưng là built-in nên rất nhẹ).

-----
### Cách mình hay dùng:

Đây là cách tận dụng tính năng của Python: Các chuỗi ký tự nằm trong dấu ngoặc đơn `()` sẽ tự động nối lại với nhau.

```python
def get_prompt_v1():
    prompt = (
        "You are an AI assistant.\n"   # Phải nhớ thêm \n
        "Your task is to analyze.\n"
        "Be concise."
    )
    return prompt
```

  * **Ưu điểm:** Không cần import thư viện, code thẳng hàng.
  * **Nhược điểm:** Phải thủ công thêm `\n` cuối mỗi dòng. Quên là chuỗi bị dính chùm.


**Và đây là áp dụng thay đổi**

```python
import openai
import os
import logging

logger = logging.getLogger(__name__)

class DeepSeekService:
    def __init__(self):
        # Khởi tạo OpenAI client với Azure config
        self.client = openai.OpenAI(
            api_key=os.getenv("AZURE_API_KEY"),
            base_url="https://DeepSeek-R1-xacdm.eastus.models.ai.azure.com"
        )
        self.model = "deepseek-chat"

    def generate_response(self, prompt: str) -> str:
        try:
            logger.info("Sending request to DeepSeek API")
            
            # Áp dụng Implicit Concatenation tại đây
            system_prompt = (
                "You are an AI assistant with expertise in AI, Machine Learning, and Software Development.\n"
                "Answer questions based on the provided CV context.\n"
                "DO NOT include any thinking process or notes to yourself in your response.\n"
                "Provide direct, concise answers only."
            )

            messages = [
                {"role": "system", "content": system_prompt},
                {"role": "user", "content": prompt}
            ]

            response = self.client.chat.completions.create(
                model=self.model,
                messages=messages,
                max_tokens=1000,
                temperature=0.7
            )

            # Lấy response content
            return response.choices[0].message.content
```
Có thể thấy code đã gọn hơn, mình cũng đọc được các rule chính dễ dàng hơn


Hy vọng bài viết này giúp các bạn có thêm một số phương pháp và chọn được công cụ phù hợp cho dự án của mình. Happy Coding\!

