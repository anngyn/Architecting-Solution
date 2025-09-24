---
title: "Tạo Lambda Function để đọc từ SQS và ghi vào DynamoDB"
weight: 6.1
chapter: false
pre: " <b> 6.1 </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ tạo một **Lambda function** để đọc các message từ **SQS queue** và ghi bản ghi đơn hàng vào **DynamoDB table**.

---

### Tạo Lambda Function với role Lambda-SQS-DynamoDB

1. Trong ô tìm kiếm của **AWS Management Console**, nhập **Lambda** và từ danh sách chọn **Lambda**.  
![image](/images/6-CreateLambdaFunction/01-findlambda.png)  
2. Chọn **Create function** và cấu hình như sau:  
   - **Function option:** Author from scratch  
   - **Function name:** `POC-Lambda-1`  
   - **Runtime:** Python 3.9  
![image](/images/6-CreateLambdaFunction/02-configlambda.png)  

   - **Change default execution role:** Use an existing role  
   - **Existing role:** `Lambda-SQS-DynamoDB`  
3. Chọn **Create function**.  

![image](/images/6-CreateLambdaFunction/03-createlambda.png)  

---

### Thiết lập Amazon SQS làm trigger để gọi Lambda function

1. Nếu cần, mở rộng phần **Function overview**.  
2. Chọn **Add trigger**.  
![image](/images/6-CreateLambdaFunction/04-trigger.png)  
3. Với **Trigger configuration**, nhập **SQS** và chọn dịch vụ từ danh sách.  
4. Với **SQS queue**, chọn `POC-Queue`.  
5. Thêm trigger bằng cách chọn **Add**.  
![image](/images/6-CreateLambdaFunction/05-addtrigger.png)  

---

### Thêm và triển khai mã Lambda function

1. Trên trang **POC-Lambda-1**, trong tab **Code**, thay thế mã mặc định bằng đoạn sau:  

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

2. Chọn **Deploy**.  
![image](/images/6-CreateLambdaFunction/06-CODE.png)  

ℹ️ **Lưu ý:** Lambda function sẽ thực thi đoạn code bạn chỉ định khi trigger được kích hoạt.  
AWS Lambda tự động quản lý tài nguyên tính toán như bộ nhớ, CPU và mạng.

---

### Kiểm thử Lambda Function POC-Lambda-1

1. Trong tab **Test**, tạo một sự kiện mới với cấu hình sau:  
   - **Event name:** `POC-Lambda-Test-1`  
   - **Template (Optional):** SQS  
2. Template SQS sẽ xuất hiện trong trường **Event JSON**.  
3. Lưu thay đổi và chọn **Test**.  
![image](/images/6-CreateLambdaFunction/07-savetest.png)  
4. Sau khi function chạy thành công, thanh thông báo sẽ hiển thị:  
   **“Execution result: succeeded”**.  
   Điều này xác nhận rằng Lambda function đã gửi test message **“Hello from SQS!”** từ template SQS đến DynamoDB table.  
![image](/images/6-CreateLambdaFunction/08-success.png)  

---

### Xác minh kết quả Lambda function trong DynamoDB

1. Trong **AWS Management Console**, nhập **DynamoDB** và chọn **DynamoDB** từ danh sách.  
2. Trong bảng điều hướng, chọn **Explore items**.  
3. Chọn bảng **orders**.  
4. Trong **Items returned**, bảng `orders` hiển thị bản ghi chứa **“Hello from SQS!”** được ghi bởi Lambda function test.  
![image](/images/6-CreateLambdaFunction/09-check.png)  

---

🔒 **Ghi chú bảo mật:** Khi gán function với role `Lambda-SQS-DynamoDB`, quyền truy cập được giới hạn chính xác theo nhu cầu — đọc từ **SQS** và ghi vào **DynamoDB** — tuân thủ nguyên tắc **least privilege**.
