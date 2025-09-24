---
title: "Kiểm thử Kiến trúc bằng API Gateway"
weight: 8
chapter: false
pre: " <b> 8. </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ sử dụng **API Gateway** để gửi dữ liệu giả lập (mock data) vào **Amazon SQS** như một bước kiểm chứng (proof of concept) cho giải pháp serverless.

---

### Gửi Yêu cầu Kiểm thử

1. Trong **API Gateway console**, quay lại trang **POST - Method Execution** và chọn **Test**.  
2. Trong ô **Request Body**, nhập:  

    ```json
    {  
      "item": "latex gloves",
      "customerID": "12345"
    }
    ```

3. Chọn **Test**.  
![image](/images/8-TestingtheArchitecture/8.test.png)  

---

### Xác minh Kết quả

- Nếu bạn thấy thông báo **“Successfully completed execution”** với mã phản hồi **200** trong logs bên phải, bạn cũng sẽ nhận được **email thông báo** chứa bản ghi mới.  
![image](/images/8-TestingtheArchitecture/9.result.png)  
- Nếu bạn không nhận được email nhưng bản ghi mới xuất hiện trong **DynamoDB table**, hãy xem lại và khắc phục từ bước sau khi cấu hình **DynamoDB**.  
- Đảm bảo rằng tất cả tài nguyên đều được triển khai trong Region **us-east-1**.  
![image](/images/8-TestingtheArchitecture/10.result.png)  

---

### Luồng Xử lý End-to-End

Sau khi **API Gateway** xử lý thành công yêu cầu:  

1. API Gateway đưa yêu cầu vào **SQS queue**.  
2. Do đã cấu hình Amazon SQS làm trigger cho Lambda đầu tiên, **SQS sẽ kích hoạt Lambda function**.  
3. Lambda function đầu tiên ghi entry mới vào **DynamoDB table**.  
4. **DynamoDB Streams** ghi nhận thay đổi trong bảng và kích hoạt Lambda thứ hai.  
5. Lambda thứ hai lấy bản ghi mới từ **DynamoDB Streams** và gửi nó đến **Amazon SNS**.  
6. **Amazon SNS** chuyển tiếp **email thông báo** tới endpoint đã đăng ký.  

---

🔒 **Ghi chú bảo mật:**  
Bài kiểm thử end-to-end này xác nhận toàn bộ **pipeline serverless** (API Gateway → SQS → Lambda → DynamoDB → DynamoDB Streams → Lambda → SNS → Email) hoạt động **an toàn và đúng như mong đợi**.
