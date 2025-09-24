---
title: "Create SNS Topic and Setup Subscriptions"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

ℹ️ **Information:** In this task, you will create an **SNS topic** and set up subscriptions.  
Amazon SNS coordinates and manages delivering or sending messages to subscriber endpoints or clients.

---

### Creating a Topic in the Notification Service

1. In the **AWS Management Console**, search for **SNS** and choose **Simple Notification Service**. 
![image](/images/5-CreateSNSTopic/01-sns.png)  
2. On the **Create topic** card, enter `POC-Topic` and choose **Next step**. 
 ![image](/images/5-CreateSNSTopic/02-sns.png)  
3. In the **Details** section, keep the **Standard** topic type selected and choose **Create topic**.  
4. On the **POC-Topic** page, copy the **ARN** of the topic that you just created and save it for reference.  
   - You will need this ARN later in the exercise.  


---

### Subscribing to Email Notifications

1. On the **Subscriptions** tab, choose **Create subscription**.  
![image](/images/5-CreateSNSTopic/03-sns.png)  
2. For **Topic ARN**, verify that the box contains the ARN for `POC-Topic`.  
3. For **Protocol**, choose **Email**.  
4. For **Endpoint**, enter your email address.  
5. Choose **Create subscription**.  
![image](/images/5-CreateSNSTopic/04-sns.png)  
6. A confirmation message will be sent to the specified email address.  
7. After receiving the confirmation email, confirm the subscription.  
   - ⚠️ If you don’t receive the email within a few minutes, check your **spam** folder.  

![image](/images/5-CreateSNSTopic/05-sns.png)  
![image](/images/5-CreateSNSTopic/06-sns.png)  
---

🔒 **Security Note:**  Using Amazon SNS with email subscriptions provides an easy way to test and validate event-driven notifications before integrating with production endpoints.
