---
title: "Lưu trữ dữ liệu"
weight: 3
chapter: false
pre: "<b> 3. </b>"
---

![Overview](/fcj-ss2-workshop-003/images/31.png)

Vậy là chúng ta đã có dữ liệu từ thiết bị được gửi lên AWS IoT Core, tiếp theo chúng ta sẽ tìm cách lưu trữ những dự liệu này vào DynamoDB.

Ở phần này chúng ta sẽ có các phần sau:

- Tạo DynamoDB table.
- Tạo Rule để lưu trữ dữ liệu vào DynamoDB.
- Tạo lambda function để xử lý dữ liệu trước khi lưu vào DynamoDB.
- Tạo IoT Core Rule.

