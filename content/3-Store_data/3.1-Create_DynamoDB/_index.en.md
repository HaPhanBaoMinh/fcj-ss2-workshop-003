---
title: "Create a Table in DynamoDB"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

After our IoT devices send data to IoT Core, we will proceed to store this information. There are many ways to store this data; here, I will use DynamoDB to store it.

### 1. Create a Table in DynamoDB

Select **Create table** to create a new table.

![Overview](/fcj-ss2-workshop-003/images/32.png)

### 2. Fill in the Required Information

- **Table name**: The name of the table you want to create.
- **Primary key**: Choose the key type for the table; here I choose **Partition key** as **device_id**.
- **Add sort key**: If you want to add a sort key, select here; I will leave it as **timestamp**.

Then proceed to select **Create** to create the table.

![Overview](/fcj-ss2-workshop-003/images/33.png)

We now have the table as follows:

![Overview](/fcj-ss2-workshop-003/images/34.png) 
