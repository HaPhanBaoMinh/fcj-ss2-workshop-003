---
title: "Chuẩn bị data mẫu"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

Để thuận tiện và đỡ tốn thời gian cho việc chuẩn bị data, chúng ta sẽ sử dụng một số data mẫu có sẵn và tiến hàn import vào DynamoDB.

### 1. Tạo S3 bucket

Đầu tiên, chúng ta cần tạo một S3 bucket để lưu trữ các file data mẫu.

Sau đó chúng ta tải file data mẫu về và upload lên S3 bucket.

![Overview](/images/48.png)

![Overview](/images/49.png)

### 2. Import data vào DynamoDB

Tiếp theo, chúng ta sẽ import data từ S3 bucket vào DynamoDB.

Chúng ta vào **DynamoDB** và chọn **Imports from S3**.

![Overview](/images/50.png)

![Overview](/images/51.png)

![Overview](/images/52.png)

Chúng ta điền thông tin như sau:

![Overview](/images/53.png)

Sau đó chúng ta tiến hành import.

Và kết quả chúng ta tạo được một table có dữ liệu mẫu.

![Overview](/images/54.png)

Như các bạn thấy, chúng ta đã có dữ liệu mẫu trong DynamoDB.

![Overview](/images/55.png)
