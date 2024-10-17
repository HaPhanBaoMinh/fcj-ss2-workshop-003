---
title: "Tạo bảng trong DynamoDB"
weight: 1
chapter: false
pre: "<b> 3.1. </b>"
---

Sau khi các thiết bị IoT của chúng ta gửi data lên cho IoT core chúng ta sẽ tiến hành lưu các thông tin này lại, có nhiều các để lưu trữ thông tin này, ở đây mình dùng DynamoDb để lưu trữ các dữ liệu trên.

### 1. Tạo bảng trong DynamoDB

Tiến hành chọn **Create table** để tạo bảng mới.

![Overview](/fcj-ss2-workshop-003/images/32.png)

### 2. Điền các thông tin cần thiết

- **Table name**: Tên bảng mà bạn muốn tạo.
- **Primary key**: Chọn kiểu key cho bảng, ở đây mình chọn **Partition key** là **device_id**.
- **Add sort key**: Nếu bạn muốn thêm sort key thì chọn vào đây, ở đây mình để là **timestamp**

Sau đó tiến hành chọn **Create** để tạo bảng.

![Overview](/fcj-ss2-workshop-003/images/33.png)

Chúng ta được bảng như sau:

![Overview](/fcj-ss2-workshop-003/images/34.png) 
