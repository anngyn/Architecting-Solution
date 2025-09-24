---
title: "Tạo API với Amazon API Gateway"
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ tạo một **REST API** trong **Amazon API Gateway**.  
API sẽ đóng vai trò như một cổng giao tiếp giữa ứng dụng của bạn và các dịch vụ AWS.

---

### Tạo REST API

1. Trong **AWS Management Console**, tìm kiếm và mở **API Gateway**.  
![image](/images/7-CreateAPIGateway/1-search.png)  
2. Trên thẻ **REST API** (có public authentication), chọn **Build** và cấu hình như sau:  
   - **Choose the protocol:** REST  
   - **Create new API:** New API  
   - **API name:** `POC-API`  
   - **Endpoint Type:** Regional  
3. Chọn **Create API**.  
![image](/images/7-CreateAPIGateway/2-create.png)  

---

### Cấu hình phương thức POST

1. Trên menu **Actions**, chọn **Create Method**.  
![image](/images/7-CreateAPIGateway/3-createmethod.png)  
2. Mở menu method bằng cách chọn mũi tên xuống và chọn **POST**.  
3. Lưu thay đổi bằng cách nhấn dấu check.  
4. Trong khung **POST - Setup**, cấu hình như sau:  
   - **Integration type:** AWS Service  
![image](/images/7-CreateAPIGateway/4-config.png)  
   - **AWS Region:** ap-southeast-1  
   - **AWS Service:** Simple Queue Service (SQS)  
   - **AWS Subdomain:** để trống  
   - **HTTP method:** POST  
   - **Action Type:** Use path override  
   - **Path override:** `<account ID>/POC-Queue`  
     - ⚠️ Ví dụ: Nếu `POC-Queue` là tên SQS queue, thì mục nhập sẽ như sau:  
       ```
       /123456789012/POC-Queue
       ```
   - **Execution role:** Dán ARN của role `APIGateway-SQS`  
     - Ví dụ:  
       ```
       arn:aws:iam::<account ID>:role/APIGateway-SQS
       ```
   - **Content Handling:** Passthrough  
![image](/images/7-CreateAPIGateway/5-config.png)  

5. Với **Request body passthrough**, chọn **Never**.  
6. Cuộn xuống cuối trang và mở rộng phần **HTTP Headers**.  
7. Chọn **Add header**.  
   - **Name:** Content-Type  
   - **Mapped from:** `'application/x-www-form-urlencoded'`  

8. Chọn **Add mapping template**.  
   - **Content-Type:** `application/json`  
9. Với **Generate template**, không chọn template mặc định.  
   - Thay vào đó, nhập lệnh sau vào ô:  
     ```
     Action=SendMessage&MessageBody=$input.body
     ```  
10. Lưu thay đổi bằng cách nhấn dấu check.  
![image](/images/7-CreateAPIGateway/7-add.png)  
