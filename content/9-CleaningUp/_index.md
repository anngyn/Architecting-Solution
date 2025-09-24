---
title: "Clean Up Resources"
weight: 9
chapter: false
pre: " <b> 9. </b> "
---

ℹ️ **Information:** In this task, you will delete all **AWS resources** that you created during this exercise to avoid unnecessary costs.

---

### Deleting the DynamoDB Table

1. Open the **DynamoDB console**.  
2. In the navigation pane, choose **Tables**.  
3. Select the `orders` table.  
4. Choose **Delete** and confirm your actions.  

---

### Deleting the Lambda Functions

1. Open the **Lambda console**.  
2. Select the Lambda functions created in this exercise:  
   - `POC-Lambda-1`  
   - `POC-Lambda-2`  
3. Choose **Actions → Delete**.  
4. Confirm your actions and close the dialog box.  

---

### Deleting the SQS Queue

1. Open the **Amazon SQS console**.  
2. Select the queue created in this exercise:  
   - `POC-Queue`  
3. Choose **Delete** and confirm your actions.  

---

### Deleting the SNS Topic and Subscriptions

1. Open the **Amazon SNS console**.  
2. In the navigation pane, choose **Topics**.  
3. Select `POC-Topic`.  
4. Choose **Delete** and confirm your actions.  
5. In the navigation pane, choose **Subscriptions**.  
6. Select the subscription created in this exercise and choose **Delete**.  
7. Confirm your actions.  

---

### Deleting the API

1. Open the **API Gateway console**.  
2. Select `POC-API`.  
3. Choose **Actions → Delete**.  
4. Confirm your actions.  

---

### Deleting the IAM Roles and Policies

1. Open the **IAM console**.  
2. In the navigation pane, choose **Roles**.  
3. Delete the following roles and confirm your actions:  
   - `APIGateway-SQS`  
   - `Lambda-SQS-DynamoDB`  
   - `Lambda-DynamoDBStreams-SNS`  

4. In the navigation pane, choose **Policies**.  
5. Delete the following custom policies and confirm your actions:  
   - `Lambda-DynamoDBStreams-Read`  
   - `Lambda-SNS-Publish`  
   - `Lambda-Write-DynamoDB`  
   - `Lambda-Read-SQS`  

---

🎉 **Congratulations!**  
You have successfully completed the exercise and cleaned up all AWS resources.  
