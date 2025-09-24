---
title: "Create Lambda Function to Publish Message to SNS Topic"
weight: 6.2
chapter: false
pre: " <b> 6.2 </b> "
---

ℹ️ **Information:** In this task, you will create a **Lambda function** for the `Lambda-DynamoDBStreams-SNS` role.  
This function uses **DynamoDB Streams** as a trigger to pass the record of a new entry to **Amazon SNS**.

---

### Creating the POC-Lambda-2 Function

1. In the **AWS Management Console**, search for and open **AWS Lambda**.  
2. Choose **Create function** and configure the following settings:  
   - **Function option:** Author from scratch  
   - **Function name:** `POC-Lambda-2`  
   - **Runtime:** Python 3.9  
   - **Change default execution role:** Use an existing role  
   - **Existing role:** `Lambda-DynamoDBStreams-SNS`  
     - This role grants permissions to get records from **DynamoDB Streams** and send them to **Amazon SNS**.  
3. Choose **Create function**.  
![image](/images/6-CreateLambdaFunction/10-create2.png) 
![image](/images/6-CreateLambdaFunction/11-config.png) 
---

### Setting up DynamoDB as a Trigger

1. In the **Function overview** section, choose **Add trigger**.  
2. Configure the trigger as follows:  
   - **Trigger configuration:** DynamoDB  
   - **DynamoDB table:** `orders`  
3. Keep the remaining default settings and choose **Add**.  
4. In the **Configuration** tab, verify that you are in the **Triggers** section and that the DynamoDB state is **Enabled**.  
![image](/images/6-CreateLambdaFunction/12-trigger.png) 
---

### Configuring the Function Code

1. On the **Code** tab, replace the Lambda function code with the following:

    ```python
    import boto3, json

    client = boto3.client('sns')

    def lambda_handler(event, context):
        for record in event["Records"]:
            if record['eventName'] == 'INSERT':
                new_record = record['dynamodb']['NewImage']    
                response = client.publish(
                    TargetArn='<Enter Amazon SNS ARN for the POC-Topic>',
                    Message=json.dumps({'default': json.dumps(new_record)}),
                    MessageStructure='json'
                )
    ```

   ⚠️ **Note:** Replace the value of `TargetArn` with the **ARN** of the Amazon SNS `POC-Topic`.  
      - Make sure to remove the placeholder angle brackets (`<>`).  
      - Example ARN:  
      ```
      arn:aws:sns:us-east-1:<account ID>:POC-Topic
      ```

2. Choose **Deploy**.  
![image](/images/6-CreateLambdaFunction/13-code.png) 
---

### Testing the POC-Lambda-2 Function

1. In the **Test** tab, create a new event with the following settings:  
   - **Event name:** `POC-Lambda-Test-2`  
   - **Template (Optional):** DynamoDB → select `DynamoDB-Update`  
2. The DynamoDB template appears in the **Event JSON** box.  
3. Save your changes and choose **Test**.  
![image](/images/6-CreateLambdaFunction/14-savetesy.png) 
4. After the function runs successfully, the notification banner shows:  
   **“Execution result: succeeded”**.  
5. Within a few minutes, an email message should arrive at the address you subscribed to in the previous task.  
   - Confirm that you received the message.  
   - If not, check your **spam folder**.  
![image](/images/6-CreateLambdaFunction/15-success.png) 
![image](/images/6-CreateLambdaFunction/16-non.png) 
---

   🔒 **Security Note:**  This Lambda function follows the principle of least privilege by using the `Lambda-DynamoDBStreams-SNS` role.  It only has the necessary permissions to read from **DynamoDB Streams** and publish messages to **SNS**.
