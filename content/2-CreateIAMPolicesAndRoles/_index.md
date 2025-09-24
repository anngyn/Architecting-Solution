---
title: "Create IAM Policies and Roles"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

### Overview
ℹ️ **Information:** In this section, we need to configure the appropriate access permissions.  
Before launching resources, we must set up **IAM Policies** and **IAM Roles** to manage access in a secure and efficient way.

---

### Required Resources
To properly configure the environment, we will create the following AWS resources:

- **IAM Policies:** JSON documents that define specific permissions, such as allowing or denying certain actions on AWS resources.  
- **IAM Roles:** An IAM identity with specific permissions. IAM Roles allow trusted entities (such as users, AWS services, or applications) to temporarily assume these permissions to perform a specific task.

⚠️ **Warning:** Properly configuring IAM Policies and IAM Roles is critical for both security and functionality.  
Misconfiguration can result in:
- Services or users not having sufficient permissions to operate  
- Worse, granting excessive permissions, which can introduce potential security vulnerabilities  

---

### Workshop Modules
Follow these steps to prepare your environment:

1. [Create an **IAM Policy**.](2.1-CreateCustomIAMPolices/)  
2. [Create an **IAM Role** and attach the **IAM Policy**.](2.2-CreateIAMRoles/)  

---

### 🔒 Security Note
IAM Policies allow us to apply the **principle of least privilege**.  
We will configure policies to:
- Grant only the necessary permissions required by our application  
- Deny all unnecessary access  
