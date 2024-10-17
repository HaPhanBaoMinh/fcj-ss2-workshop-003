---
title: "Create Lambda"
weight: 2
chapter: false
pre: "<b> 3.2. </b>"
---

We will create a lambda function to process the data before storing it in DynamoDB.

### 1. Create Lambda Function

- Access **Lambda** on the AWS console.
- Select **Create function** to create a new lambda function.
  
![Overview](/fcj-ss2-workshop-003/images/35.png)

### 2. Fill in the Required Information

- **Function name**: The name of the lambda function.
- **Runtime**: Choose the runtime for the lambda function; here I select **Python 3.11**.
- Then select **Create function** to create the lambda function.

![Overview](/fcj-ss2-workshop-003/images/36.png)

### 3. Update the Role of the Lambda Function

For the lambda function to access DynamoDB, we need to update the role of the lambda function.

- We can click here to navigate to the IAM role page of the lambda function.

![Overview](/fcj-ss2-workshop-003/images/37.png)

### 4. Add Policy

- Here we will add a new policy for the lambda function.
- To make it easier, we will select the policy **AmazonDynamoDBFullAccess**.

![Overview](/fcj-ss2-workshop-003/images/38.png)

![Overview](/fcj-ss2-workshop-003/images/39.png)

### 5. Update Code for the Lambda Function

- We will update the code for the lambda function as follows:

```python
import json
import boto3
from botocore.exceptions import ClientError

# Initialize DynamoDB
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('ESP32-Temperature-Humidity')

def lambda_handler(event, context):
    try:
        # Retrieve data from event
        device_id = event['device_id']
        temperature = event['temp']
        humidity = event['humidity']
        timestamp = event['timestamp']
        
        # Save data to DynamoDB
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