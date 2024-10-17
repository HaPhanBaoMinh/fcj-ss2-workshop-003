---
title: "MQTT Test Client"
weight: 3
chapter: false
pre: "<b> 2.3. </b>"
---

We will use the MQTT test client to test the connection between the device and AWS IoT Core.

### 1. In the console screen, select **MQTT test client**.

![Overview](/fcj-ss2-workshop-003/images/23.png)

Here, we enter the topic as **test** and select **Subscribe to topic**.

Scroll down, and we will see a message display box. Currently, we haven't received any messages.

![Overview](/fcj-ss2-workshop-003/images/25.png)

Now, we are listening to all messages from the **test** topic. Whenever a message is published to the **test** topic, we will receive that message.

### 2. We will test by publishing a message to the **test** topic.

We will send a message to the **test** topic with the content **Hello from AWS IoT console** and select **Publish**.

![Overview](/fcj-ss2-workshop-003/images/24.png)

After publishing, we will receive the message we just published in the **Subscribe to a topic** tab.

![Overview](/fcj-ss2-workshop-003/images/26.png)

OK, good job!