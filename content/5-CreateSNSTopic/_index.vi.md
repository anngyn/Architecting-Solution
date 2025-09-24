---
title: "Tạo SNS Topic và Thiết lập Subscriptions"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

ℹ️ **Thông tin:** Trong tác vụ này, bạn sẽ tạo một **SNS topic** và thiết lập các **subscriptions**.  
Amazon SNS điều phối và quản lý việc phân phối hoặc gửi tin nhắn đến các endpoint hoặc client đăng ký nhận.

---

### Tạo Topic trong Notification Service

1. Trong **AWS Management Console**, tìm kiếm **SNS** và chọn **Simple Notification Service**.  
![image](/images/5-CreateSNSTopic/01-sns.png)  
2. Trên thẻ **Create topic**, nhập `POC-Topic` và chọn **Next step**.  
![image](/images/5-CreateSNSTopic/02-sns.png)  
3. Trong phần **Details**, giữ nguyên loại topic **Standard** và chọn **Create topic**.  
4. Trên trang **POC-Topic**, sao chép **ARN** của topic vừa tạo và lưu lại để tham chiếu sau.  
   - Bạn sẽ cần ARN này ở các bước tiếp theo của bài tập.  

---

### Đăng ký Nhận Email Notifications

1. Trên tab **Subscriptions**, chọn **Create subscription**.  
![image](/images/5-CreateSNSTopic/03-sns.png)  
2. Với **Topic ARN**, xác minh rằng hộp nhập chứa ARN của `POC-Topic`.  
3. Với **Protocol**, chọn **Email**.  
4. Với **Endpoint**, nhập địa chỉ email của bạn.  
5. Chọn **Create subscription**.  
![image](/images/5-CreateSNSTopic/04-sns.png)  
6. Một email xác nhận sẽ được gửi đến địa chỉ email bạn đã nhập.  
7. Sau khi nhận được email xác nhận, hãy bấm **Confirm subscription**.  
   - ⚠️ Nếu không nhận được email trong vài phút, hãy kiểm tra thư mục **Spam**.  

![image](/images/5-CreateSNSTopic/05-sns.png)  
![image](/images/5-CreateSNSTopic/06-sns.png)  

---

🔒 **Ghi chú bảo mật:** Sử dụng Amazon SNS với email subscriptions cung cấp một cách đơn giản để kiểm tra và xác thực **event-driven notifications** trước khi tích hợp với các endpoint trong môi trường production.
