---
title: "Tạo Lambda"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

Chún ta sẽ tạo một lambda function để xử lý dữ liệu trước khi lưu vào DynamoDB.

### 1. Tạo Lambda Function

- Truy cập vào **Lambda** trên console của AWS.
- Chọn **Create function** để tạo một lambda function mới.
  
![Overview](/images/35.png)

### 2. Điền các thông tin cần thiết

- **Function name**: Tên của lambda function.
- **Runtime**: Chọn runtime cho lambda function, ở đây mình chọn **Python 3.11**.
- Sau đó chọn **Create function** để tạo lambda function.

![Overview](/images/36.png)

### 3. Update role của lambda function

Để lambda function có thể truy cập vào DynamoDB chúng ta cần update role của lambda function.

- Chúng ta có thể click vào đây để được chuyển tới trang IAM role của lambda function.

![Overview](/images/37.png)

### 4. Thêm policy

- Ở đây chúng ta sẽ thêm một policy mới cho lambda function.
- Ở đây để thuận chúng ta sẽ chọn policy **AmazonDynamoDBFullAccess**.

![Overview](/images/38.png)

![Overview](/images/39.png)

### 5. Update code cho lambda function

- Chúng ta sẽ update code cho lambda function như sau:

```python
import json
import boto3
from botocore.exceptions import ClientError

# Khởi tạo DynamoDB
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('ESP32-Temperature-Humidity')

def lambda_handler(event, context):
    try:
        # Lấy dữ liệu từ event
        device_id = event['device_id']
        temperature = event['temp']
        humidity = event['humidity']
        timestamp = event['timestamp']
        
        # Lưu dữ liệu vào DynamoDB
        response = table.put_item(
            Item={
                'device_id': device_id,
                'temperature': temperature,
                'humidity': humidity,
                'timestamp': timestamp
            }
        )
        
        print("Data saved successfully:", response)
        return {
            'statusCode': 200,
            'body': json.dumps('Data saved successfully')
        }
    
    except ClientError as e:
        print("Error saving data:", e)
        return {
            'statusCode': 500,
            'body': json.dumps('Error saving data')
        }
    
    except KeyError as e:
        print("Missing key in event:", e)
        return {
            'statusCode': 400,
            'body': json.dumps('Missing key in event')
        }
```



