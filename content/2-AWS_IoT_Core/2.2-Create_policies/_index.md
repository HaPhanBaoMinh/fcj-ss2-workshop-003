---
title: "Tạo policy"
weight: 2
chapter: false
pre: " <b> 2.2. </b> "
---

Tiếp theo chúng ta sẽ tạo policy cho các ""things"" mà chúng ta đã tạo ở bước trước có thể truy cập các AWS IoT Core resources.

### 1. Chúng ta chọn **Create a policy**.

![Overview](/images/17.png)

### 2. Điền thông tin về policy của bạn.

Ở đây mình điền thông tin như sau:

- Policy Name: Tên của policy.
- Plicy effect: Chúng ta chọn **Allow** - cho phép.
- Policy action: Chúng ta chọn **iot:*** - cho phép tất cả các action trong AWS IoT Core.
- Resource ARN: Chúng ta chọn **All resources** - cho phép tất cả các resources trong AWS IoT Core.

Sau đó chúng ta chọn **Create**.

![Overview](/images/18.png)

### 3. Sau khi tạo chúng ta sẽ thấy policy của mình.

![Overview](/images/19.png)

### 4. Tiếp theo chúng ta sẽ gắn policy này với certificate mà chúng ta đã tạo ở bước trước.

Chúng ta vào **Certificates** và chọn **Attach policy**.

![Overview](/images/20.png)

Chúng ta chọn policy mà chúng ta vừa tạo và chọn **Attach polices**.

![Overview](/images/21.png)

### 5. Sau khi gắn policy chúng ta sẽ thấy policy đã được gắn với certificate.

![Overview](/images/22.png)

