---
title: "Chuẩn bị dataset"
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

Trước khi chúng ta bắt đầu xây dựng mô hình machine learning, chúng ta cần chuẩn bị dataset cho mô hình của mình.

Từ dữ liệu mẫu mà chúng ta đã import vào DynamoDB, chúng ta sẽ sử dụng dữ liệu này để xây dựng mô hình machine learning.

Đầu tiên chúng ta phải export dữ liệu từ DynamoDB ra file CSV như mình đã hướng dẫn ở step 4.

### 1. Tạo dataset

Chúng ta vào **Sagemaker** và chọn **Datasets** sau đó chọn **Import data**.

Chúng ta chọn **Tabular** và tiến hành chọn file CSV mà chúng ta đã export từ DynamoDB.

![Overview](/fcj-ss2-workshop-003/images/66.png)

Chúng ta có thể preview dữ liệu trước khi import.

![Overview](/fcj-ss2-workshop-003/images/67.png)

Tiến hành **Create dataset**.

![Overview](/fcj-ss2-workshop-003/images/68.png)

Kiểm tra lại ở trang **Datasets** chúng ta đã tạo được dataset.

![Overview](/fcj-ss2-workshop-003/images/69.png)