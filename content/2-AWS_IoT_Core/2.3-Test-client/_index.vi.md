---
title: "MQTT test client"
weight: 3
chapter: false
pre: "<b> 2.3. </b>"
---

Chúng ta sẽ sử dụng MQTT test client để test kết nối giữa thiết bị và AWS IoT Core.

### 1. Ở màn hình console chúng ta chọn **MQTT test client**.

![Overview](/fcj-ss2-workshop-003/images/23.png)

Ở đây chúng ta điền thông tin topic là **test** và chọn **Subscribe to topic**.

Kéo xuống dưới chúng ta sẽ thấy một khung hiển thị message, hiện tại chúng ta chưa nhận được message nào.

![Overview](/fcj-ss2-workshop-003/images/25.png)

Bây giờ chúng ta đang lắng nghe tất cả các message từ topic **test** mỗi khi có message được publish lên topic **test** thì chúng ta sẽ nhận được message đó.

### 2. Chúng ta sẽ test bằng cách publish một message lên topic **test**.

Chúng ta sẽ gửi một message lên topic **test**, với nội dung là **Hello from AWS IoT console** và chọn **Publish**.

![Overview](/fcj-ss2-workshop-003/images/24.png)

Sau khi publish chúng ta sẽ nhận được message mà chúng ta vừa publish ở tab **Subscribe to a topic**.

![Overview](/fcj-ss2-workshop-003/images/26.png)

OK good job! 

