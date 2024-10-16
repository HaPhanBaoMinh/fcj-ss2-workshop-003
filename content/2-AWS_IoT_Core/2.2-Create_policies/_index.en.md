---
title: "Create Policy"
weight: 2
chapter: false
pre: " <b> 2.2. </b> "
---

Next, we will create a policy so that the "things" we created in the previous step can access AWS IoT Core resources.

### 1. Select **Create a policy**.

![Overview](/images/17.png)

### 2. Fill in your policy details.

Here, I entered the following information:

- Policy Name: The name of the policy.
- Policy effect: Select **Allow** - to permit access.
- Policy action: Select **iot:*** - to allow all actions in AWS IoT Core.
- Resource ARN: Select **All resources** - to allow access to all resources in AWS IoT Core.

Then select **Create**.

![Overview](/images/18.png)

### 3. After creating, you will see your policy.

![Overview](/images/19.png)

### 4. Next, we will attach this policy to the certificate we created earlier.

Go to **Certificates** and select **Attach policy**.

![Overview](/images/20.png)

Select the policy you just created and choose **Attach policies**.

![Overview](/images/21.png)

### 5. After attaching, you will see the policy linked to the certificate.

![Overview](/images/22.png)

