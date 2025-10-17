---
layout: post
title:  "Cơ Bản Về Deep Learning: Giải Thích Mạng Nơ-Ron Nhân Tạo"
date:   2025-10-14 14:30:00 +0700
author: baro
categories: deep-learning neural-networks
excerpt: "Kiến thức cơ bản nhất về Deep Learning mà bạn cần biết"
image: https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Colored_neural_network.svg/640px-Colored_neural_network.svg.png
---
## Giới thiệu về Deep Learning 

Chào các bạn, đây là bài viết đầu tiên về topic **Deep Learning** của bọn mình. Trong bài viết này mình sẽ cùng đi qua một chút về khái niệm của **Deep Learning** nhé!.

Chắc hẳn các bạn đã nghe về các từ khóa như **Mạng "Nơ ron" nhân tạo**, **Thị giác máy tính**, **Xử lí ngôn ngữ tự nhiên**. Hồi mình còn bé thì mình hay có xem một số bộ phim viễn tưởng về một thế giới tràn đầy công nghệ, như phim IronMan (Mình là fan cứng của Marvel). Mình ấn tượng mãi về trợ lí thông minh của Tony Stark, trợ lý ảo thông minh Jarvis. Thật ra thì phải nói là cực cực thông minh, tuy nhiên Tony chỉ đặt cho cô một cái tên rất khiêm tốn: **Jarvis** - **Just A Rather Very Intelligent System** ( tạm dịch: Cũng chỉ là một hệ thống khá thông minh). Cô có thể giao tiếp real-time với Tony, giúp Tony chế tạo bộ giáp, quản lý công việc cho Tony, chăm lo cho đời sống của Tony và là trợ lý tìm kiếm mọi thông tin trên internet cho Tony, đôi khi còn cứu mạng Tony nữa. Đọc đến đây các bạn có thể thấy phần nào quen thuộc với cuộc sống của mình mấy năm trở lại đây đúng không!? Đúng vậy, là người bạn **ChatGPT.**

Từ một khái niệm chỉ nằm trong sách vở, giờ đây **Deep Learning** đã trở thành “bộ não” đứng sau vô số ứng dụng mà chúng ta sử dụng hằng ngày — từ công cụ tìm kiếm, dịch ngôn ngữ, xe tự hành, cho đến các trợ lý ảo thông minh như Siri, Google Assistant, hay chính ChatGPT mà bạn đang đọc đây.Có thể thấy,đây chính là ví dụ điển hình cho thấy Deep Learning đã phát triển mạnh mẽ đến mức nào trong thời đại hiện nay.

Vậy **Deep Learning** thực chất là gì?

`Nói một cách dễ hiểu, Deep Learning (Học sâu) là một nhánh của Machine Learning (Học máy) — mà bản thân Machine Learning lại là một phần của Trí tuệ nhân tạo (Artificial Intelligence - AI). Deep Learning sử dụng mạng nơ-ron nhân tạo (Artificial Neural Networks) để mô phỏng cách hoạt động của não người, từ đó giúp máy tính có thể tự học, tự rút ra quy luật, và ra quyết định mà không cần con người phải lập trình từng bước chi tiết.`

Chúng ta sẽ phân tích về cụm từ **Deep Learning**: <b><u><i> Học - Sâu</i></u></b>

`Học: Quá trình mô phỏng cách học của não người. thể hiện khả năng tự cải thiện thông qua dữ liệu và kinh nghiệm.
Trong lĩnh vực trí tuệ nhân tạo, “học” nghĩa là máy tính không chỉ làm theo lệnh có sẵn, mà tự tìm ra quy luật ẩn bên trong dữ liệu.
Ví dụ: khi bạn cho một chương trình hàng nghìn bức ảnh mèo, nó “học” cách nhận biết mèo mà không cần bạn phải nói cụ thể “mèo có tai nhọn, mắt tròn, có râu,...
`

`Sâu: ở đây không phải nói về mức độ thông minh, mà nói về độ sâu trong cấu trúc mạng nơ-ron nhân tạo.
Càng “sâu” thì mạng càng có khả năng học được những đặc trưng phức tạp và trừu tượng hơn.`

<b>Nói tóm lại: <i> “Học sâu” là quá trình máy tính học từ dữ liệu thông qua một mạng nơ-ron nhân tạo nhiều tầng, giúp nó có thể hiểu và biểu diễn thông tin ở mức độ phức tạp cao, tương tự cách bộ não con người xử lý thông tin


---

## 1️⃣ Cấu trúc của một mạng nơ-ron  
Trước hết, chúng ta sẽ xem qua một minh họa về cấu tạo của não người trước. 
Một **nơ-ron sinh học** là **tế bào thần kinh** có nhiệm vụ **truyền và xử lý thông tin** trong hệ thần kinh.  
Mỗi nơ-ron gồm 3 phần chính:

1. **Dendrite (Sợi nhánh):**  
   - Nhận tín hiệu từ các nơ-ron khác và truyền về thân tế bào.

2. **Cell body (Thân tế bào / Soma):**  
   - Nơi xử lý thông tin nhận được.  
   - Nếu tín hiệu đủ mạnh, nó sẽ kích hoạt **xung điện (action potential)** để gửi đi.

3. **Axon (Sợi trục):**  
   - Dẫn tín hiệu điện từ thân tế bào đến các nơ-ron khác.  
   - Đầu tận cùng của axon kết nối với **synapse** – nơi truyền tín hiệu sang nơ-ron kế tiếp.


`
![Nơ-ron sinh học](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b5/Neuron.svg/640px-Neuron.svg.png)

> **Giải thích hình:**  
> - Phần rẽ nhánh bên trái là **Dendrites** (tiếp nhận tín hiệu).  
> - Phần giữa là **Cell body** (xử lý thông tin).  
> - Đường dài kéo sang phải là **Axon** (truyền tín hiệu đi).  

```Khi bạn **suy nghĩ**, **ra quyết định**, hay **ghi nhớ điều gì đó**, bên trong não bạn đang diễn ra một quá trình vô cùng phức tạp — nhưng lại hết sức kỳ diệu.
- Trong não có khoảng **86 tỷ nơ-ron**, mỗi nơ-ron có thể **kết nối với hàng nghìn nơ-ron khác** thông qua các **khớp thần kinh (synapse)**.  
- Khi bạn nhìn thấy, nghe thấy hoặc cảm nhận một điều gì, các nơ-ron này **truyền tín hiệu điện** qua axon, và tại khớp synapse, tín hiệu đó được **chuyển thành tín hiệu hóa học** (neurotransmitters) để truyền sang nơ-ron tiếp theo.  

- Khi một nhóm nơ-ron được kích hoạt cùng nhau, chúng tạo thành **một mẫu (pattern)**.  
- Các mẫu này chính là **đơn vị cơ bản của suy nghĩ**.  
- Nếu các nơ-ron kích hoạt lặp lại nhiều lần cho cùng một trải nghiệm, các kết nối giữa chúng sẽ **mạnh dần lên**.  
  → Đây chính là nguyên tắc **“Neurons that fire together, wire together”** – tạm dịch: *Những nơ-ron kích hoạt cùng nhau sẽ gắn kết với nhau.
```
---

- Trong **mạng nơ-ron nhân tạo**, mỗi **nơ-ron nhân tạo** mô phỏng cơ chế này:  
  - **Input (đầu vào)** tương ứng với **tín hiệu từ dendrite**.  
  - **Hàm tính toán** tương tự **quá trình xử lý trong cell body**.  
  - **Output (đầu ra)** giống như **tín hiệu truyền qua axon** sang nơ-ron khác.  


Một **mạng nơ-ron nhân tạo (Artificial Neural Network)** được tạo thành từ nhiều **nơ-ron (neurons)** kết nối với nhau.  
Về cơ bản, mạng gồm **3 phần chính** như sau:

![Cấu trúc mạng nơ-ron cơ bản](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Colored_neural_network.svg/640px-Colored_neural_network.svg.png)

> **Giải thích:**  
> - Các chấm tròn: nơ-ron.  
> - Các đường nối: kết nối giữa các nơ-ron.  
> - Dữ liệu đi **từ trái sang phải**:  
>  - Lớp đầu vào → Lớp ẩn → Lớp đầu ra.

---

### **1. Lớp đầu vào (Input Layer)**  
- Là nơi **nhận dữ liệu ban đầu** để mạng xử lý.  
- Mỗi **nơ-ron đầu vào** đại diện cho **một đặc trưng (feature)** của dữ liệu.  

**Ví dụ:**  
Nếu ta có một ảnh đen trắng kích thước `28x28` pixel (như trong bộ dữ liệu **MNIST**), thì tổng cộng có:  **28 x 28 = 784** nơ-ron đầu vào, tương ứng với **784 giá trị điểm ảnh**.  

---

### **2. Các lớp ẩn (Hidden Layers)**  
- Đây là nơi mạng **học các đặc trưng ẩn** bên trong dữ liệu.  
- Mỗi nơ-ron trong lớp ẩn **kết nối** với tất cả các nơ-ron ở lớp trước.  
- Tại mỗi nơ-ron, dữ liệu được xử lý qua công thức:  z = f(x) với các trọng số và giá trị đầu vào

Sau đó đi qua một **hàm kích hoạt (activation function)** để tạo ra đầu ra:  

\[
a = f(z)
\]



### **3. Lớp đầu ra (Output Layer)**  
- Là nơi **cho ra kết quả cuối cùng** sau khi mạng đã xử lý toàn bộ dữ liệu.  
- Số lượng nơ-ron ở lớp này **phụ thuộc vào bài toán**:  
  - Nếu là **phân loại nhị phân** → có 1 nơ-ron (kết quả là 0 hoặc 1).  
  - Nếu là **phân loại nhiều lớp** → có `k` nơ-ron, tương ứng `k` nhãn.  

**Ví dụ:**  
Trong bài toán nhận dạng chữ số từ 0 đến 9 → ta có **10 nơ-ron đầu ra**, mỗi nơ-ron đại diện cho **một chữ số**.  

>  **Tóm lại:**  
> Dữ liệu đi vào **lớp đầu vào**, được **xử lý qua các lớp ẩn**, và cuối cùng **ra kết quả ở lớp đầu ra**.  
> Mạng nơ-ron càng “sâu” (nhiều lớp ẩn) thì khả năng học của nó càng mạnh.


---

<u><i>Trong các **bài viết sau**, chúng ta sẽ tìm hiểu sâu hơn về phần này nhé.







---

