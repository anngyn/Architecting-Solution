---
title: "Create Amazon SQS Queue"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

ℹ️ **Information:** In this task, you will create an **Amazon SQS queue**.  
In the architecture for this exercise, **Amazon SQS** receives data records from **API Gateway**, stores them, and then sends them to a database.

---

### Creating the Queue

1. In the **AWS Management Console** search box, enter **SQS** and from the list, choose **Simple Queue Service**.  
2. On the **Get started** card, choose **Create queue**.  
![image](/images/4-CreateSQSQueue/01-sqs.png)  
3. The **Create queue** page appears.  
4. Configure the following settings:  
   - **Name:** `POC-Queue`  
   - **Access Policy:** Basic  
![image](/images/4-CreateSQSQueue/02-sqs.png) 

---

### Configuring Permissions

- **Define who can send messages to the queue**  
  - Select **Only the specified AWS accounts, IAM users and roles**.  
  - In the box, paste the Amazon Resource Name (ARN) for the **APIGateway-SQS IAM role**.  
    - Example:  
      ```
      arn:aws:iam::<account ID>:role/APIGateway-SQS
      ```

- **Define who can receive messages from the queue**  
  - Select **Only the specified AWS accounts, IAM users and roles**.  
  - In the box, paste the ARN for the **Lambda-SQS-DynamoDB IAM role**.  
    - Example:  
      ```
      arn:aws:iam::<account ID>:role/Lambda-SQS-DynamoDB
      ```
![image](/images/4-CreateSQSQueue/03-sqs.png) 
---

### Final Step

- Choose **Create queue**.  

---

🔒 **Security Note:**  By restricting the **send** permission to API Gateway and the **receive** permission to the Lambda function, you ensure that the queue is used only by the intended services, enforcing the **principle of least privilege**.
