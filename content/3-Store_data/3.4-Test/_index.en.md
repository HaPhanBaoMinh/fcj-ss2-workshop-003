---
title: "Test"
weight: 4
chapter: false
pre: "<b> 3.4. </b>"
---

It seems everything is set up correctly. Now let's try powering on the ESP32 and see if the data gets saved to DynamoDB.

- When the ESP32 runs, the data will be sent to AWS IoT Core.
- AWS IoT Core will process the data and store it in DynamoDB.
- We will check if the data has been saved to DynamoDB.

![Overview](/fcj-ss2-workshop-003/images/46.png)

![Overview](/fcj-ss2-workshop-003/images/47.png)

As you can see, the data has been saved to DynamoDB.
