---
title: "Prepare Dataset"
weight: 1
chapter: false
pre: "<b> 5.1. </b>"
---

Before we start building our machine learning model, we need to prepare the dataset for our model.

Using the sample data that we imported into DynamoDB, we will use this data to build the machine learning model.

First, we need to export the data from DynamoDB to a CSV file as I instructed in step 4.

### 1. Create Dataset

We go to **SageMaker** and select **Datasets**, then choose **Import data**.

We select **Tabular** and proceed to choose the CSV file that we exported from DynamoDB.

![Overview](/fcj-ss2-workshop-003/images/66.png)

We can preview the data before importing.

![Overview](/fcj-ss2-workshop-003/images/67.png)

Proceed to **Create dataset**.

![Overview](/fcj-ss2-workshop-003/images/68.png)

Check back on the **Datasets** page, and we see that we have successfully created the dataset.

![Overview](/fcj-ss2-workshop-003/images/69.png)
