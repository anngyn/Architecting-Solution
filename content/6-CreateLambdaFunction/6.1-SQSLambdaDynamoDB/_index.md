---
title: "Create Lambda Function for read message from SQS and write record to DynamoDB"
weight: 6.1
chapter: false
pre: " <b> 6.1 </b> "
---

ℹ️ **Information:** In this task, you will create a **Lambda function** that reads messages from the **SQS queue** and writes an order record to the **DynamoDB table**.

---

### Creating a Lambda function for the Lambda-SQS-DynamoDB role

1. In the **AWS Management Console** search box, enter **Lambda** and from the list, choose **Lambda**.  
![image](/images/6-CreateLambdaFunction/01-findlambda.png)  
2. Choose **Create function** and configure the following settings:  
   - **Function option:** Author from scratch  
   - **Function name:** `POC-Lambda-1`  
   - **Runtime:** Python 3.9  
![image](/images/6-CreateLambdaFunction/02-configlambda.png)  

   - **Change default execution role:** Use an existing role  
   - **Existing role:** `Lambda-SQS-DynamoDB`  
3. Choose **Create function**.  

![image](/images/6-CreateLambdaFunction/03-createlambda.png)  

---

### Setting up Amazon SQS as a trigger to invoke the function

1. If needed, expand the **Function overview** section.  
2. Choose **Add trigger**.  
![image](/images/6-CreateLambdaFunction/04-trigger.png)  
3. For **Trigger configuration**, enter **SQS** and choose the service from the list.  
4. For **SQS queue**, choose `POC-Queue`.  
5. Add the trigger by choosing **Add**.  
![image](/images/6-CreateLambdaFunction/05-addtrigger.png) 

---

### Adding and deploying the function code

1. On the **POC-Lambda-1** page, in the **Code** tab, replace the default Lambda function code with the following:

    ```python
    import boto3, uuid

    client = boto3.resource('dynamodb')
    table = client.Table("orders")

    def lambda_handler(event, context):
        for record in event['Records']:
            print("test")
            payload = record["body"]
            print(str(payload))
            table.put_item(Item= {
                'orderID': str(uuid.uuid4()),
                'order': payload
            })
    ```

2. Choose **Deploy**.  
![image](/images/6-CreateLambdaFunction/06-CODE.png) 
ℹ️ **Note:**  
The Lambda function executes the code you specify when the trigger is invoked.  
AWS Lambda automatically manages compute resources such as memory, CPU, and networking.

---

### Testing the POC-Lambda-1 function

1. In the **Test** tab, create a new event with the following settings:  
   - **Event name:** `POC-Lambda-Test-1`  
   - **Template (Optional):** SQS  
2. The SQS template appears in the **Event JSON** field.  
3. Save your changes and choose **Test**.  
![image](/images/6-CreateLambdaFunction/07-savetest.png) 
4. After the function runs successfully, the notification banner shows:  
   **“Execution result: succeeded”**.  
   This confirms that the Lambda function sent the test message **“Hello from SQS!”** from the SQS template to the DynamoDB table.  
![image](/images/6-CreateLambdaFunction/08-success.png) 
---

### Verifying the Lambda function output in DynamoDB

1. In the **AWS Management Console** search box, enter **DynamoDB** and choose **DynamoDB** from the list.  
2. In the navigation pane, choose **Explore items**.  
3. Select the **orders** table.  
4. Under **Items returned**, the `orders` table shows the record containing **“Hello from SQS!”** that was written by the Lambda function test.  
![image](/images/6-CreateLambdaFunction/09-check.png) 
---

🔒 **Security Note:**  By associating the function with the role `Lambda-SQS-DynamoDB`, permissions are restricted to exactly what the function needs — reading from **SQS** and writing to **DynamoDB** — following the **principle of least privilege**.
