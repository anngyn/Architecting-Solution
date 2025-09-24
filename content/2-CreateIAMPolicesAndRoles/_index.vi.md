---
title: "Tạo IAM Policies và Roles"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

### Tổng quan
ℹ️ **Thông tin:** Trong phần này, chúng ta cần cấu hình các quyền truy cập phù hợp.  
Trước khi khởi chạy tài nguyên, chúng ta phải thiết lập **IAM Policies** và **IAM Roles** để quản lý truy cập một cách an toàn và hiệu quả.

---

### Các tài nguyên cần thiết
Để cấu hình môi trường một cách chính xác, chúng ta sẽ tạo các tài nguyên AWS sau:

- **IAM Policies:** Các tài liệu JSON định nghĩa quyền cụ thể, chẳng hạn như cho phép hoặc từ chối một hành động nào đó trên tài nguyên AWS.  
- **IAM Roles:** Một danh tính IAM với các quyền cụ thể. IAM Roles cho phép các thực thể đáng tin cậy (như người dùng, dịch vụ AWS hoặc ứng dụng) tạm thời đảm nhận các quyền này để thực hiện một tác vụ cụ thể.

⚠️ **Cảnh báo:** Cấu hình **IAM Policies** và **IAM Roles** đúng cách là rất quan trọng đối với cả bảo mật và chức năng.  
Cấu hình sai có thể dẫn đến:  
- Dịch vụ hoặc người dùng không có đủ quyền để hoạt động  
- Nghiêm trọng hơn, cấp quá nhiều quyền, có thể tạo ra lỗ hổng bảo mật tiềm tàng  

---

### Các module của Workshop
Hãy làm theo các bước sau để chuẩn bị môi trường của bạn:

1. [Tạo một **IAM Policy**.](2.1-CreateCustomIAMPolices/)  
2. [Tạo một **IAM Role** và gắn với **IAM Policy**.](2.2-CreateIAMRoles/)  

---

### 🔒 Ghi chú về bảo mật
IAM Policies cho phép chúng ta áp dụng **nguyên tắc quyền tối thiểu (least privilege)**.  
Chúng ta sẽ cấu hình các policy để:  
- Chỉ cấp các quyền cần thiết cho ứng dụng của chúng ta  
- Từ chối tất cả các quyền truy cập không cần thiết  
