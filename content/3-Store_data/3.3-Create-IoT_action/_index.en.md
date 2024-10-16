---
title: "Create IoT Rule and Action"
weight: 3
chapter: false
pre: "<b> 3.3. </b>"
---

We will create an IoT rule and action to send information from IoT Core to the Lambda function.

### 1. Create IoT Rule

- Access **IoT Core** on the AWS console.
- Select **Message routing** and then select **Rules**.
- Choose **Create rule**. 

![Overview](/images/40.png)

### 2. Fill in the Required Information

- **Name**: The name of the rule.
- **Description**: A description of the rule.

![Overview](/images/41.png)

- Fill in the information for the query statement:

![Overview](/images/42.png)

- In the **Set one or more actions** section, select **Add action**.
- Choose the **Lambda** function that we created in the previous step.

![Overview](/images/43.png)

- Review the information and proceed to create the rule.

![Overview](/images/44.png)

At this point, when you return to the Lambda function page, you will see a new trigger created.

![Overview](/images/45.png)
