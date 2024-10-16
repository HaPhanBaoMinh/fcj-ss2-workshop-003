---
title: "Device Registration"
weight: 1
chapter: false
pre: " <b> 2.1. </b> "
---

The first step to using AWS IoT Core is registering a device. In our case, it's the ESP32.

### 1. Access [AWS IoT Core](https://console.aws.amazon.com/iot/home?region=us-east-1#/dashboard) and select **Create thing**.

![Overview](/fcj-ss2-workshop-003/images/11.png)
### 2. Fill in the details of your device. In this example, I entered the following information:

Besides the device name, you will see additional fields such as:

- Thing type: Type of device.
- Thing group: Device group.
- Billing group: Billing group.
- Packages and versions: Version and package.

These details help you manage your devices more efficiently, especially if you have many devices.

Here, I enter the device name + device ID.

Afterward, select **Next**.

![Overview](/fcj-ss2-workshop-003/images/12.png)

### 3. Create Certificates.

To ensure the data sent and received is secure, we need to generate certificates for the device.

Here, I choose **Auto-generate a new certificate** and then select **Next**.

![Overview](/fcj-ss2-workshop-003/images/13.png)

### 4. Attach a policy.

We will create the policy later, so in this step, select **Create thing**.

![Overview](/fcj-ss2-workshop-003/images/14.png)

### 5. After creation, download the certificate files to your computer.

![Overview](/fcj-ss2-workshop-003/images/15.png)

![Overview](/fcj-ss2-workshop-003/images/16.png)

