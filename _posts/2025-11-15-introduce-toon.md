---
layout: post
title: "TOON là gì? Hướng dẫn đơn giản cho người mới về định dạng dữ liệu tiết kiệm token cho AI"
date: 2025-11-15 22:31:00 +0700
author: baro
categories: [ai, machine-learning]
tags: [llm, json, data-format, beginner]
image: https://community.n8n.io/uploads/default/optimized/3X/5/b/5b8f2fc9337995ea1f9b2f0b50232870b295f385_2_690x344.png
excerpt: "Bạn mới làm quen với AI và LLM? TOON giúp bạn gửi dữ liệu JSON vào prompt mà không tốn nhiều token. Bài viết này giải thích đơn giản, với ví dụ dễ theo dõi, để bạn nhanh chóng áp dụng."
---

![TOON logo with step-by-step guide](https://github.com/toon-format/toon/raw/main/.github/og.png)

# TOON là gì? Hướng dẫn đơn giản cho người mới về định dạng dữ liệu tiết kiệm token cho AI

Chào bạn! Nếu bạn đang học về AI, đặc biệt là Large Language Models (LLM) như ChatGPT hay Grok, bạn có thể đã nghe về "token". Token là đơn vị cơ bản mà AI dùng để hiểu văn bản – giống như từ hoặc phần từ. Mỗi token tốn tiền và giới hạn dung lượng prompt (câu hỏi bạn gửi cho AI).

Hôm nay, mình giới thiệu **TOON (Token-Oriented Object Notation)** – một cách viết dữ liệu JSON đơn giản, ngắn gọn hơn để gửi vào AI. TOON giống như "phiên bản nhẹ" của JSON, giúp tiết kiệm token (thường 30-60% ít hơn) mà vẫn giữ nguyên thông tin. Nó đặc biệt hữu ích khi bạn gửi danh sách dữ liệu lớn, như danh sách người dùng hoặc sản phẩm.

Đừng lo nếu bạn mới bắt đầu: Mình sẽ giải thích từng bước, với ví dụ dễ hiểu. Không cần kiến thức lập trình sâu!

## Tại sao cần TOON? (Vấn đề với JSON thông thường)
Khi làm việc với AI, bạn thường gửi dữ liệu dạng JSON (một định dạng phổ biến cho dữ liệu có cấu trúc). Nhưng JSON "dài dòng" vì có nhiều dấu ngoặc `{ }`, dấu phẩy `,`, và dấu ngoặc kép `" "`. Điều này làm tốn token không cần thiết.

**Ví dụ đơn giản:** Giả sử bạn có danh sách 2 người dùng:

**JSON thông thường** (dài, tốn ~45 token):
```json
{
  "users": [
    { "id": 1, "name": "Alice", "role": "admin" },
    { "id": 2, "name": "Bob", "role": "user" }
  ]
}
```

YAML (ngắn hơn một chút, ~35 token):
```yaml
users:
  - id: 1
    name: Alice
    role: admin
  - id: 2
    name: Bob
    role: user
```

**TOON** (ngắn nhất, ~25 token):
```
users[2]{id,name,role}:
  1,Alice,admin
  2,Bob,user
```

- `[2]` nghĩa là có 2 phần tử.
- `{id,name,role}` là các trường dữ liệu (chỉ viết một lần!).
- Dòng dưới là dữ liệu theo hàng, như bảng Excel.

Kết quả? Bạn gửi được nhiều dữ liệu hơn vào AI mà không tốn kém!

## Tính năng chính của TOON (Dễ dùng cho người mới)
TOON được thiết kế để dễ đọc và dễ viết, giống như kết hợp YAML (dễ đọc) và CSV (bảng dữ liệu):

- **Tiết kiệm token:** Ít dấu thừa, đặc biệt với danh sách lớn (arrays uniform – tức tất cả item giống cấu trúc).
- **Dễ theo dõi:** Dùng khoảng trắng để lồng (indentation), không cần ngoặc lồng nhau.
- **Hỗ trợ AI tốt:** AI dễ "hiểu" cấu trúc nhờ số lượng rõ ràng (`[N]`) và tên trường (`{fields}`).
- **Linh hoạt:** Chọn dấu phân cách (`,`, tab, hoặc `|`) để tối ưu.

TOON không thay thế JSON hoàn toàn – dùng JSON cho code, TOON cho prompt AI.

## Khi nào dùng TOON? (Và khi nào không)
**Dùng TOON khi:**
- Bạn có danh sách dữ liệu giống nhau, như: danh sách nhân viên, sản phẩm, hoặc log sự kiện.
- Muốn gửi dữ liệu lớn vào AI để hỏi (ví dụ: "Tìm nhân viên có lương > 50k").

**Không dùng khi:**
- Dữ liệu lồng phức tạp (nhiều level con) – dùng JSON compact.
- Dữ liệu phẳng hoàn toàn (không có trường) – dùng CSV.
- Cần tốc độ cao nhất – test thử xem JSON có nhanh hơn không.

## Benchmarks đơn giản: TOON tiết kiệm bao nhiêu?
Dựa trên test với 4 AI model (Claude, Gemini, GPT, Grok) và 11 bộ dữ liệu:

- **Accuracy (độ chính xác AI hiểu dữ liệu):** TOON 73.9% (cao hơn JSON 69.7%).
- **Token tiết kiệm:** 
  - Với danh sách phẳng: 59% ít hơn JSON.
  - Với dữ liệu lồng: 22% ít hơn.

Ví dụ thực tế (dữ liệu thời gian, 60 ngày):
- JSON: 22,250 token.
- TOON: 9,120 token (**tiết kiệm 59%**).

TOON giúp AI trả lời đúng hơn vì cấu trúc rõ ràng, giảm lỗi khi đọc dữ liệu lớn.

## Bắt đầu với TOON: Cài đặt và thử ngay
### Không cần cài: Dùng CLI qua npx
Mở terminal (Command Prompt trên Windows) và thử:
```bash
# Chuyển JSON thành TOON
echo '{"users": [{"id":1,"name":"Alice"}]}' | npx @toon-format/cli
```
Kết quả:
```
users[1]{id,name}:
  1,Alice
```

### Cài library (nếu dùng code)
Nếu bạn code JavaScript/TypeScript:
```bash
npm install @toon-format/toon
```

Ví dụ code đơn giản:
```javascript
const { encode } = require('@toon-format/toon');
const data = {
  users: [
    { id: 1, name: 'Alice', role: 'admin' },
    { id: 2, name: 'Bob', role: 'user' }
  ]
};
console.log(encode(data));
```
Output:
```
users[2]{id,name,role}:
  1,Alice,admin
  2,Bob,user
```

### Thử online
- [TOON Tools](https://toontools.vercel.app/): Paste JSON, xem TOON ngay.
- [Token Playground](https://www.curiouslychase.com/playground/format-tokenization-exploration): So sánh token.

## Tổng quan format: Cách đọc/viết TOON
### Object đơn giản
```
id: 123
name: Ada
active: true
```

### Danh sách (Array)
- **Danh sách đơn giản:** `tags[3]: admin,ops,dev`
- **Danh sách bảng (tabular):** 
```
items[2]{sku,qty,price}:
  A1,2,9.99
  B2,1,14.5
```

### Dấu ngoặc kép (Quoting)
TOON chỉ dùng ngoặc kép khi cần (ví dụ: có dấu phẩy trong text: `"hello, world"`). Điều này tiết kiệm token!

## Dùng TOON trong prompt AI
Gửi TOON vào AI như thế này (dùng code block):
````
Dữ liệu dưới dạng TOON (danh sách người dùng):
```toon
users[2]{id,name,role}:
  1,Alice,admin
  2,Bob,user
```
Hỏi: Ai là admin? Trả lời ngắn gọn.
````
AI sẽ dễ hiểu và trả lời chính xác hơn!

Để AI tạo TOON: "Tạo danh sách users theo TOON, dùng header `users[N]{id,name}:`".

## Lưu ý cho người mới
- TOON dành cho input AI, không phải lưu trữ dữ liệu.
- Nếu dữ liệu không uniform (khác cấu trúc), TOON fallback sang dạng list như YAML.
- Test token của bạn: Dùng playground để so sánh.

## Kết luận
Có thể coi TOON là sự kết hợp giữa csv và yaml, . Mình sẽ nghiên cứu thêm về định dạng này, trong các bài viết tiếp theo hi vọng chúng ta có thể bắt đầu bằng ví dụ nhỏ, rồi áp dụng cho dự án thực tế như phân tích log hoặc query database.



*(Nguồn: Dựa trên spec TOON v2.0 tại [GitHub](https://github.com/toon-format/toon).)*

---