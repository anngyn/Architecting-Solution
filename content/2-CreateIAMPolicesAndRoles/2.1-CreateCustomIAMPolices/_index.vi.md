---
title: "Tạo IAM Policies"
weight: 2.1
chapter: false
pre: " <b> 2.1 </b> "
---

ℹ️ **Thông tin:** Trong phần này, chúng ta sẽ tạo một **IAM Policy** chuyên biệt để giới hạn quyền truy cập tới các dịch vụ AWS cụ thể. Cụ thể, policy này sẽ được cấu hình cho **AWS Lambda**, **Amazon DynamoDB** và **Amazon SQS**. Việc cấu hình đúng cách sẽ giúp kiểm soát truy cập và tăng cường bảo mật.

---

### Các bước tạo IAM Policies 
1. Tạo **Lambda-Write-DynamoDB**  
    - Trong thanh tìm kiếm, gõ *IAM*, sau đó chọn *IAM* từ danh sách dịch vụ.  
![IAM Searching](/images/2-CreateIAMPolicesAndRoles/010-IAM.png)

    - Trong thanh điều hướng của **IAM dashboard**, chọn **Policies**.  
![IAM Policies](/images/2-CreateIAMPolicesAndRoles/02-Polices.png)

    - Chọn **Create Policy**:
        - Bạn có thể tạo và chỉnh sửa policy bằng visual editor hoặc dùng JSON. Trong bài thực hành này, chúng ta cung cấp các đoạn JSON để tạo policy. Tổng cộng, bạn cần tạo 4 policy.
        - Trong tab **JSON**, dán đoạn mã sau:
    ```json
    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "dynamodb:PutItem",
                "dynamodb:DescribeTable"
            ],
            "Resource": "*"
        }
    ]
    }
    ```
    - Chọn **Next:** để review policy.  
![Json](/images/2-CreateIAMPolicesAndRoles/03-Create.jpeg)

        - Đoạn JSON này cấp quyền cho phép ghi dữ liệu (`PutItem`) vào DynamoDB và xem thông tin bảng (`DescribeTable`). Ký tự hoa thị (*) cho biết các hành động này áp dụng cho **tất cả các tài nguyên**.

    - Đặt tên cho policy là `Lambda-Write-DynamoDB`.  

    - Chọn **Create policy**.  
![Create](/images/2-CreateIAMPolicesAndRoles/04-Createpolicy.png)

---

2. Sau khi tạo **Lambda-Write-DynamoDB**, lặp lại các bước trên để tạo các policy sau:

    - Policy cho **Amazon SNS**: cho phép publish, get, và list các topic được Lambda sử dụng.  
        - **Tên:** `Lambda-SNS-Publish`  
        - **JSON:**
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": [
                    "sns:Publish",
                    "sns:GetTopicAttributes",
                    "sns:ListTopics"
                ],
                "Resource": "*"
            }
        ]
    }
    ```

    - Policy cho **DynamoDB Streams**: cho phép Lambda đọc các bản ghi từ DynamoDB Streams.  
        - **Tên:** `Lambda-DynamoDBStreams-Read`  
        - **JSON:**
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": [
                    "dynamodb:GetShardIterator",
                    "dynamodb:DescribeStream",
                    "dynamodb:ListStreams",
                    "dynamodb:GetRecords"
                ],
                "Resource": "*"
            }
        ]
    }
    ```

    - Policy cho **Amazon SQS**: cho phép Lambda đọc các message từ SQS queue.  
        - **Tên:** `Lambda-Read-SQS`  
        - **JSON:**
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": [
                    "sqs:DeleteMessage",
                    "sqs:ReceiveMessage",
                    "sqs:GetQueueAttributes",
                    "sqs:ChangeMessageVisibility"
                ],
                "Resource": "*"
            }
        ]
    }
    ```
