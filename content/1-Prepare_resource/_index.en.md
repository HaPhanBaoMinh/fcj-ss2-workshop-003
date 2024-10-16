---
title: "Preparation"
weight: 1
chapter: false
pre: "<b> 1. </b>"
---

![Overview](/fcj-ss2-workshop-003/images/01.png)

## Overview Diagram

The diagram above shows an overview of this lab.

1. The ESP32 will collect temperature and humidity data from the sensor.
2. The ESP32 will send the collected information to the AWS IoT Core Service via the MQTT protocol with the corresponding topic.
3. After receiving the information from the ESP32, AWS IoT Core will send that data to AWS Lambda for processing.
4. AWS Lambda will store the received information in DynamoDB.
5. After a certain period, we will use the data in DynamoDB to import into Amazon SageMaker Canvas to create graphs and predict temperature and humidity.

## Resource Information

All setup information for Wokwi and code can be found here: [Resources](https://github.com/HaPhanBaoMinh/fcj-ss2-workshop-003-resource)
