---
title: "Chuẩn bị data mẫu"
weight: 4
chapter: false
pre: "<b> 4. </b>"
---

Để thuận tiện và đỡ tốn thời gian cho việc chuẩn bị data, chúng ta sẽ sử dụng một số data mẫu có sẵn và tiến hàn import vào DynamoDB.

### 1. Tạo S3 bucket

Đầu tiên, chúng ta cần tạo một S3 bucket để lưu trữ các file data mẫu.

Sau đó chúng ta tải file data mẫu về và upload lên S3 bucket.

![Overview](/fcj-ss2-workshop-003/images/48.png)

![Overview](/fcj-ss2-workshop-003/images/49.png)

### 2. Import data vào DynamoDB

Tiếp theo, chúng ta sẽ import data từ S3 bucket vào DynamoDB.

Chúng ta vào **DynamoDB** và chọn **Imports from S3**.

![Overview](/fcj-ss2-workshop-003/images/50.png)

![Overview](/fcj-ss2-workshop-003/images/51.png)

![Overview](/fcj-ss2-workshop-003/images/52.png)

Chúng ta điền thông tin như sau:

![Overview](/fcj-ss2-workshop-003/images/53.png)

Sau đó chúng ta tiến hành import.

Và kết quả chúng ta tạo được một table có dữ liệu mẫu.

![Overview](/fcj-ss2-workshop-003/images/54.png)

Như các bạn thấy, chúng ta đã có dữ liệu mẫu trong DynamoDB.

![Overview](/fcj-ss2-workshop-003/images/55.png)

### 3. Export data từ DynamoDB

Chúng ta cũng có thể export data từ DynamoDB ra file CSV để tiến hành import Dataset vào SageMaker.

Trong mục **Explore items** sau khi **Scan** chúng ta chọn **Action** và chọn **Download results to CSV**.

![Overview](/fcj-ss2-workshop-003/images/65.png)

