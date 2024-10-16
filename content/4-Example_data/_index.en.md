---
title: "Preparing Sample Data"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

To make the data preparation process easier and save time, we will use some available sample data and proceed to import it into DynamoDB.

### 1. Create an S3 Bucket

First, we need to create an S3 bucket to store the sample data files.

Next, we download the sample data file and upload it to the S3 bucket.

![Overview](/fcj-ss2-workshop-003/images/48.png)

![Overview](/fcj-ss2-workshop-003/images/49.png)

### 2. Import Data into DynamoDB

Next, we will import data from the S3 bucket into DynamoDB.

We go to **DynamoDB** and select **Imports from S3**.

![Overview](/fcj-ss2-workshop-003/images/50.png)

![Overview](/fcj-ss2-workshop-003/images/51.png)

![Overview](/fcj-ss2-workshop-003/images/52.png)

We fill in the information as follows:

![Overview](/fcj-ss2-workshop-003/images/53.png)

After that, we proceed to import.

As a result, we create a table with sample data.

![Overview](/fcj-ss2-workshop-003/images/54.png)

As you can see, we have sample data in DynamoDB.

![Overview](/fcj-ss2-workshop-003/images/55.png)

### 3. Export Data from DynamoDB

We can also export data from DynamoDB to a CSV file to import the dataset into SageMaker.

In the **Explore items** section, after performing a **Scan**, we select **Action** and choose **Download results to CSV**.

![Overview](/fcj-ss2-workshop-003/images/65.png)
