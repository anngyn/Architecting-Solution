---
title: "Create IAM Roles"
weight: 2.2
chapter: false
pre: " <b> 2.2 </b> "
---

ℹ️ **Information:** Because AWS follows the principle of **least privilege**, we recommend providing role-based access only to the AWS resources required to perform a task. In this step, you will create **IAM Roles** and attach policies to them.

---

### Step by step IAM Roles Creation

1. **Create IAM Role for Lambda (DynamoDB + SQS)**  
    - In the navigation pane of the **IAM dashboard**, choose **Roles**.  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/01-policy.png)
    - Choose **Create role** and configure the following settings on the **Select trusted entity** page:  
        - **Trusted entity type:** AWS service  
        - **Common use cases:** Lambda  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/02-role.png)
    - Choose **Next**.  
    - On the **Add permissions** page, select:  
        - `Lambda-Write-DynamoDB`  
        - `Lambda-Read-SQS`  
    ![Roles](/images/2-CreateIAMPolicesAndRoles/03-roles.png)
    - Choose **Next**.  
    - For **Role name**, enter: `Lambda-SQS-DynamoDB`  
    - Choose **Create role**.
    ![Roles](/images/2-CreateIAMPolicesAndRoles/04-roles.jpg)

---

2. **Create IAM Role for Lambda (DynamoDB Streams + SNS)**  
    - Follow the same steps above and use the following settings:  
        - **IAM role name:** `Lambda-DynamoDBStreams-SNS`  
        - **Trusted entity type:** AWS service  
        - **Common use cases:** Lambda  
        - **Attach policies:**  
            - `Lambda-SNS-Publish`  
            - `Lambda-DynamoDBStreams-Read`  

---

3. **Create IAM Role for API Gateway (SQS + CloudWatch)**  
    - Follow the same steps above and use the following settings:  
        - **IAM role name:** `APIGateway-SQS`  
        - **Trusted entity type:** AWS service  
        - **Common use cases:** API Gateway  
        - **Attach policies:**  
            - `AmazonAPIGatewayPushToCloudWatchLogs`  

---

🔒 **Security Note:**  Assigning policies only to the roles that require them enforces the **principle of least privilege**, ensuring Lambda and API Gateway have just enough access to perform their tasks and nothing more.
