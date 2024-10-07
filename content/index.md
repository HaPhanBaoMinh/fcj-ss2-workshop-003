---
title: "Giới thiệu"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

# Dự Đoán Nhiệt Độ & Độ Ẩm Từ Dữ Liệu ESP32 qua IoT Core

![Overview](/images/00.png)

## 1. Overview

Trong bài viết này, chúng ta sẽ tìm hiểu cách sử dụng ESP32 để đo nhiệt độ và độ ẩm từ cảm biến nhiệt độ, độ ẩm, sau đó gửi dữ liệu lên AWS IOT CORE và lưu trữ vào DynamoDB. Sau đó chúng ta sẽ dùng Lambda để chuẩn hóa dữ liệu. Cuối cùng, chúng ta sẽ sử dụng AWS SageMaker Canvas để tiến hành dự đoán nhiệt độ và độ ẩm trong tương lai.

Bài Lab này có thể ứng dụng trong nhiều lĩnh vực như: nông nghiệp, y tế, công nghiệp, ...

## 2. Objectives
- Hiểu cách sử dụng ESP32 để đo nhiệt độ và độ ẩm từ cảm biến nhiệt độ, độ ẩm
- Hiểu cách gửi dữ liệu lên AWS IOT CORE và lưu trữ vào DynamoDB
- Hiểu cách sử dụng Lambda để chuẩn hóa dữ liệu
- Hiểu cách sử dụng AWS SageMaker Canvas để tiến hành dự đoán nhiệt độ và độ ẩm trong tương lai

## 3. Content
- [1. Chuẩn bị các tài nguyên cần thiết](/chapter1)
- [2. Cài đặt ESP32](/chapter2)
- [3. Gửi dữ liệu lên AWS IOT CORE](/chapter3)
- [4. Lưu trữ dữ liệu vào DynamoDB](/chapter4)
- [5. Chuẩn hóa dữ liệu bằng Lambda](/chapter5)
- [6. Dự đoán nhiệt độ và độ ẩm bằng SageMaker Canvas](/chapter6)
- [7. Kết luận và xóa các service](/chapter7)
