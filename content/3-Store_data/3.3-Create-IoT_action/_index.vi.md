---
title: "Tạo IoT rule và action"
weight: 3
chapter: false
pre: "<b> 3.3. </b>"
---

Chúng ta sẽ tạo một IoT rule và action để gửi thông tin từ IoT Core tới Lambda function.

### 1. Tạo IoT rule

- Truy cập vào **IoT Core** trên console của AWS.
- Chọn **Message routing** và chọn **Rules**.
- Chọn **Create rule**. 

![Overview](/images/40.png)


### 2. Điền các thông tin cần thiết

- **Name**: Tên của rule.
- **Description**: Mô tả về rule.

![Overview](/images/41.png)

- Điền thông tin về query statement:

![Overview](/images/42.png)

- Ở phần **Set one or more actions** chọn **Add action**.
- Chọn **Lambda** mà chúng ta đã tạo ở bước trước đó.

![Overview](/images/43.png)

- Review lại thông tin và tiến hành tạo.

![Overview](/images/44.png)

Lúc này khi quay lại trang Lambda function chúng ta sẽ thấy được một trigger mới được tạo.

![Overview](/images/45.png)

