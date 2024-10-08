---
title: "Đăng kí thiết bị"
weight: 1
chapter: false
pre: " <b> 2.1. </b> "
---

Bước đầu tiên để sử dụng AWS IoT Core là chúng ta cần đăng kí một thiết bị. Trong trường hợp của chúng ta thì đó là ESP32.

### 1. Chúng ta tuy cập vào [AWS IoT Core](https://console.aws.amazon.com/iot/home?region=us-east-1#/dashboard) và chọn **Create thing**.

![Overview](/images/11.png)

### 2. Điền thông tin về thiết bị của bạn. Ở đây mình điền thông tin như sau:

Ở đây ngoài tên thì còn có nhiều thông tin khác như:

- Thing type: Loại thiết bị.
- Thing group: Nhóm thiết bị.
- Billing group: Nhóm thanh toán.
- Packages and versions: Phiên bản và gói.

Những thông tin này sẽ giúp bạn quản lý thiết bị của mình một cách dễ dàng hơn trong trường hợp bạn có nhiều thiết bị.

Ở đây mình điền tên thiết bị + mã số thiết bị.

Sau đó các bạn chọn **Next**.

![Overview](/images/12.png)

### 3. Tạo Certificates.

Để đảm bảo thông tin gửi đi và nhận về an toàn, chúng ta cần tạo Certificates cho thiết bị.

Ở đây mình chọn **Auto-generate a new certificate** và chọn **Next**.

![Overview](/images/13.png)

### 4. Attach a policy.

Chúng ta sẽ tạo policy sau, ở bước này chúng ta chọn **Create thing**

![Overview](/images/14.png)

### 5. Sau khi tạo chúng ta hãy tải các file Certificates về máy.

![Overview](/images/15.png)

![Overview](/images/16.png)



