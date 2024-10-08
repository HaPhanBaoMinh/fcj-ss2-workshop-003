---
title: "Chuẩn bị tài nguyên"
weight: 1
chapter: false
pre: "<b> 1. </b>"
---

![Overview](/images/01.png)

## Sơ đồ tổng quan

Sơ đồ trên là sơ đồ tổng quan về bài lab này. 

1. ESP32 sẽ thu thập thông tin về nhiệt độ và độ ẩm từ cảm biến.
2. ESP32 sẽ gửi thông tin thu thập được lên Service AWS IoT Core thông qua giao thức MQTT với topic tương ứng, ở đây topic sẽ được chia theo cấu trúc `device_id/sensor_id`.
3. Sau khi nhận được thông tin từ ESP32, AWS IoT Core sẽ gửi thông tin đó đến AWS Lambda để xử lý.
4. AWS Lambda sẽ lưu thông tin nhận được vào DynamoDB.
5. Sau một khoảng thời gian chúng ta sẽ sử dụng dữ liệu trong DynamoDB để import vào Amazon SageMaker Canvas để vẽ biểu đồ và dự đoán nhiệt độ và độ ẩm.

## Thông tin về resourre
Toàn bộ thông tin setup wokwi và code mình sẽ để ở đây: [Tài nguyên]()