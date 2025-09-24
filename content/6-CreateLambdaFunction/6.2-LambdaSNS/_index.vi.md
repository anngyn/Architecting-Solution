---
title: "Tạo Lambda Function để Publish Message lên SNS Topic"
weight: 6.2
chapter: false
pre: " <b> 6.2 </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ tạo một **Lambda function** với role `Lambda-DynamoDBStreams-SNS`.  
Hàm này sử dụng **DynamoDB Streams** làm trigger để chuyển bản ghi của một entry mới sang **Amazon SNS**.

---

### Tạo Function POC-Lambda-2

1. Trong **AWS Management Console**, tìm và mở **AWS Lambda**.  
2. Chọn **Create function** và cấu hình như sau:  
   - **Function option:** Author from scratch  
   - **Function name:** `POC-Lambda-2`  
   - **Runtime:** Python 3.9  
   - **Change default execution role:** Use an existing role  
   - **Existing role:** `Lambda-DynamoDBStreams-SNS`  
     - Role này cấp quyền lấy bản ghi từ **DynamoDB Streams** và gửi chúng đến **Amazon SNS**.  
3. Chọn **Create function**.  
![image](/images/6-CreateLambdaFunction/10-create2.png)  
![image](/images/6-CreateLambdaFunction/11-config.png)  

---

### Thiết lập DynamoDB làm Trigger

1. Trong phần **Function overview**, chọn **Add trigger**.  
2. Cấu hình trigger như sau:  
   - **Trigger configuration:** DynamoDB  
   - **DynamoDB table:** `orders`  
3. Giữ nguyên các thiết lập mặc định còn lại và chọn **Add**.  
4. Trong tab **Configuration**, kiểm tra mục **Triggers** và xác nhận rằng trạng thái DynamoDB là **Enabled**.  
![image](/images/6-CreateLambdaFunction/12-trigger.png)  

---

### Cấu hình Function Code

1. Trong tab **Code**, thay thế đoạn code mặc định bằng code sau:  

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

   ⚠️ **Lưu ý:** Thay giá trị `TargetArn` bằng **ARN** của SNS `POC-Topic`.  
      - Hãy xóa dấu ngoặc nhọn `< >`.  
      - Ví dụ ARN:  
      ```
      arn:aws:sns:us-east-1:<account ID>:POC-Topic
      ```

2. Chọn **Deploy**.  
![image](/images/6-CreateLambdaFunction/13-code.png)  

---

### Kiểm thử Function POC-Lambda-2

1. Trong tab **Test**, tạo một sự kiện mới với các thiết lập sau:  
   - **Event name:** `POC-Lambda-Test-2`  
   - **Template (Optional):** DynamoDB → chọn `DynamoDB-Update`  
2. Template DynamoDB sẽ xuất hiện trong ô **Event JSON**.  
3. Lưu thay đổi và chọn **Test**.  
![image](/images/6-CreateLambdaFunction/14-savetesy.png)  
4. Sau khi function chạy thành công, thanh thông báo hiển thị:  
   **“Execution result: succeeded”**.  
5. Trong vài phút, một email sẽ được gửi tới địa chỉ bạn đã đăng ký trong bước trước.  
   - Xác nhận rằng bạn đã nhận được email.  
   - Nếu không, hãy kiểm tra thư mục **Spam**.  
![image](/images/6-CreateLambdaFunction/15-success.png)  
![image](/images/6-CreateLambdaFunction/16-non.png)  

---

🔒 **Ghi chú bảo mật:** Lambda function này tuân thủ nguyên tắc **least privilege** bằ
