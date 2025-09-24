---
title: "Create Lambda Function"
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

### Overview
ℹ️ **Information:** In this section, we will create **AWS Lambda functions** to handle the serverless workflow.  
Lambda will act as the compute layer that processes messages from **Amazon SQS**, writes records into **DynamoDB**, and forwards database changes to **Amazon SNS** via **DynamoDB Streams**.

---

### Required Resources
To properly configure the environment, we will build the following Lambda functions:

- **POC-Lambda-1:** Reads messages from the SQS queue and inserts records into the DynamoDB table.  
- **POC-Lambda-2:** Uses DynamoDB Streams as a trigger and publishes new records to an SNS topic.  

⚠️ **Warning:** Lambda functions require the correct **execution roles**.  
Misconfigured roles can result in:  
- Failure to read messages from SQS  
- Failure to write data to DynamoDB  
- Failure to publish events to SNS  

---

### Workshop Modules
Follow these steps to prepare Lambda for the workshop:

1. [Create the **Lambda function** to process messages from SQS and write to DynamoDB.](6.1-SQSLambdaDynamoDB/)  
2. [Create the **Lambda function** to publish DynamoDB Stream records to SNS.](6.2-DynamoDBStreamstoSNS/)  

---

### 🔒 Security Note
Always follow the **principle of least privilege** when assigning IAM roles to Lambda.  
Each function should only have permissions required for its specific task:
- **POC-Lambda-1:** Access to read from SQS and write to DynamoDB  
- **POC-Lambda-2:** Access to read from DynamoDB Streams and publish to SNS  
