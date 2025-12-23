---
layout: post
title: "Numpy fundamental - Chia sẻ tài liệu giảng dạy về buổi dạy Numpy cho lớp Python Fundamental"
date: 2025-12-01 22:31:00 +0700
author: baro
categories: [ai, machine-learning]
tags: [llm, data-format, beginner]
image: https://user-images.githubusercontent.com/67586773/105037297-c8bd5900-5a83-11eb-801e-d382e69ec071.jpeg
excerpt: "Bạn mới làm quen với AI và LLM? TOON giúp bạn gửi dữ liệu JSON vào prompt mà không tốn nhiều token. Bài viết này giải thích đơn giản, với ví dụ dễ theo dõi, để bạn nhanh chóng áp dụng."
---

![Numpy](https://user-images.githubusercontent.com/67586773/105037297-c8bd5900-5a83-11eb-801e-d382e69ec071.jpeg)

#Mở đầu

Chào các bạn, mình là BaroDev. Tháng 7 vừa qua mình có dạy một lớp Python Fundamental (định hướng ML). Hôm nay mình xin chia sẻ lại một chút kiến thức về buổi dạy. Mình xin chia sẻ file notebook của chủ đề <b>Sơ lược cơ bản về thư viện Numpy.<b>



Đừng lo nếu bạn mới bắt đầu, thư viện này rất lớn, đến tận bây giờ mình vẫn chưa khai phá được hết khả năng của nó. Trong bài viết này sẽ cover được phần nào những gì mình có thể tận dụng được từ thư viện, ở mức độ cơ bản.

1. Numpy package core của mọi tính toán trên python

Trong python, khi làm việc với các tính toán đại số trên ma trận và véc tơ thì chúng ta chủ yếu sử dụng numpy. Numpy là viết tắt của cụm từ numerical python tức là thư viện số học của Python. Chính vì vậy các chức năng chính của thư viện này tập trung vào hỗ trợ và tối ưu các tính toán trên dữ liệu mảng nhiều chiều (multidimensional array). Numpy có những ưu điểm giúp cho nó hoạt động nhanh hơn trên python như:

    Được phát triển trên interface của C nên khắc phục được sự chậm chạp của xử lý đơn luồng trên python.

    Các dữ liệu trên numpy array được lưu trữ trên những vùng ô nhớ liền kề nên có tốc độ truy xuất rất nhanh.

    Các hàm tính toán đại số được tối ưu để cho tốc độ cao.

Ngoài ra numpy còn là thư viện được sử dụng nhiều trong các packages khác nằm trong hệ sinh thái machine learning của python như scikit-learn, scipy, pandas, matplotlib nên package này rất thuận tiện trong việc xử lý dữ liệu và huấn luyện mô hình.

Qua bài viết này chúng a sẽ cùng tìm hiểu những chức năng chính của numpy để giúp nó trở thành một thư viện toàn năng được sử dụng trong các tính toán đại số trên python.

2. Khởi tạo một mảng trên numpy

2.1. Khởi tạo ngay từ đầu

Để khởi tạo một mảng trên numpy chúng ta sử dụng câu lệnh rất quen thuộc là np.array(). Numpy cho phép chúng ta khởi tạo mảng được cấu hình theo định dạng dữ liệu cụ thể như float, interger, boolean, string. Chúng ta cũng lưu ý rằng các phần tử của một mảng trong numpy phải đồng nhất về định dạng dữ liệu.

```python 
import numpy as np

A = np.array([[1, 2],
              [3, 4]])

print(A)
print("dtype of matrix A: ", A.dtype)
```
Và đây là output
```
output
[[1 2]
 [3 4]]
dtype of matrix A:  int64
```

3. Ứng dụng của hàm SEED()

Các bạn hay chơi tài xỉu chắc chắn biết về tính random của mỗi phiên chơi. Nhưng liệu các bạn có biết về nguyên lý hoạt động đằng sau nó.

-----------------------------------------------------------------------------------
<b>Vừa rồi là preview nhanh về nội dung của bài chia sẻ này. Để đọc chi tiết và thực hành, mình sẽ để link notebook ở đây. 

*[Notebook](https://colab.research.google.com/drive/1Yjx4E1KSztzrsV5HYFoEdTNCm5KLR3oI?usp=sharing#scrollTo=Z-PCe_bk-HXK)*

---