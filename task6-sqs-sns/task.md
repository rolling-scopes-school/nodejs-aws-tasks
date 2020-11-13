# Task 6 (AWS SQS/SNS)

**After Lecture 6 "Lecture 6: SNS subscription to file upload + SQS chunk post to Lambda"**

## Prerequisites
---

- The task is a continuation of Homework 5 and should be done in the same repos


## TASK 6.1
---

Create an SQS queue, called **catalogItemsQueue**, in the resources section in **serverless.yml** file.
Update the **importFileParser** lambda function to send each CSV record into SQS.

## TASK 6.2
---

Create a lambda function called **catalogItemProcess** which will be triggered by the SQS **catalogItemsQueue**.
Configure the SQS to trigger lambda **catalogItemProcess** with 5 messages at once via batchSize property.
The lambda function should iterate over all SQS messages and create corresponding products in the products table.
The response should be a correct HTTP response code.

## TASK 6.3
---

Create an SNS topic **createProductTopic** and subscription in the resources section in **serverless.yml**.
Update the **catalogItemProcess** lambda function to send an email once it creates products.


## Evaluation criteria
---

Reviewers should verify the lambda functions by invoking them through provided URLs.
 
- **1** - File **serverless.yml** contains policies to allow lambda **catalogItemProcess** function to interact with SNS and SQS
- **3** - File **serverless.yml** contains configuration for SNS Topic **createProductTopic** 
- **4** - File **serverless.yml** contains configuration for SQS **catalogItemsQueue**


## Additional (optional) tasks
---

- **+1** - **catalogItemProcess** lambda is covered by **unit** tests 
- **+1** - set a Filter Policy  for SNS **createProductTopic** in **serverless.yml**
- **+2** - set a Redrive Policy with a Dead Letter Queue for SNS **createProductTopic** in **serverless.yml**

