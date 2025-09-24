---
title: "Create IAM Policies"
weight: 2.1
chapter: false
pre: " <b> 2.1 </b> "
---

ℹ️**Information:** In this section, we will create a specialized IAM Policy to restrict access to specific AWS services. Specifically, the policy will be configured for AWS Lambda, Amazon DynamoDB, and Amazon SQS. Proper configuration of this policy will enforce access control and enhance security.

### Step by step IAM Policies Creation 
1. Create Lambda-Write-DynamoDB. 
    - In the searchbar, type *IAM*, then select *IAM* from the services list
![IAM Searching](/images/2-CreateIAMPolicesAndRoles/010-IAM.png)

    - In the navigation pane of the **IAM dashboard**, choose **Policies**.
![IAM Policies](/images/2-CreateIAMPolicesAndRoles/02-Polices.png)
    - Choose **Create Policy**:
        - You can create and edit a policy in the visual editor or use JSON. In this exercise, we provide JSON scripts to create policies. In total, you must create four policies.
        - In the JSON tab, paste the following code:
    ```
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
    - Choose **Next:** to review the policy.
![Json](/images/2-CreateIAMPolicesAndRoles/03-Create.jpeg)
        - This JSON script grants permissions to put items into the DynamoDB table. The asterisk (*) indicates that the specified actions can apply to all available resources.
    - For the policy name, enter `Lambda-Write-DynamoDB`.

    - Choose **Create** policy.
![Create](/images/2-CreateIAMPolicesAndRoles/04-Createpolicy.png)

2. After you create the **Lambda-Write-DynamoDB** policy, repeat the previous steps to create the following policies:
    - A policy for Amazon SNS to get, list, and publish topics that are received by Lambda:

        - Name: `Lambda-SNS-Publish`
        - JSON:
    ```
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

    - A policy for Lambda to get records from DynamoDB Streams:

        - Name: `Lambda-DynamoDBStreams-Read`
        - JSON:
    ```
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

    - A policy for Lambda to read messages that are placed in Amazon SQS:

        - Name: `Lambda-Read-SQS`
        - JSON:

    ```
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