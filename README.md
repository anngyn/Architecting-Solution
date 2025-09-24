# Architecting Solution on AWS

This repository contains a comprehensive workshop guide for **Architecting Solutions on AWS**, designed for AWS First Cloud Journey (FCJ) students and cloud enthusiasts.

> **Note**: This workshop follows best practices for AWS architecture design and implementation.

---

## 📌 Overview

- **Framework**: [Hugo](https://gohugo.io/) static site generator
- **Theme**: Based on Grav Learn Theme
- **Purpose**: Learn AWS architecture patterns and implementation
- **Level**: Intermediate to Advanced

---

## 🚀 Getting Started

### Prerequisites

- AWS Account with appropriate permissions
- Basic understanding of AWS services
- Hugo installed on your local machine

### 1. Clone this repository

```bash
git clone https://github.com/anngyn/Architecting-Solution.git
cd Architecting-Solution
```

### 2. Run the workshop locally

1. Install Hugo following the [Hugo installation guide](https://gohugo.io/installation/)
2. Verify installation:

```bash
hugo version
```

3. Start the local server:

```bash
hugo server
```

4. Open your browser and go to [http://localhost:1313](http://localhost:1313)

### 3. Workshop Content

This workshop covers:

- **IAM Policies and Roles** - Security best practices
- **DynamoDB** - NoSQL database setup and streaming
- **SQS** - Message queuing service
- **SNS** - Notification service
- **Lambda Functions** - Serverless computing
- **API Gateway** - RESTful API creation
- **Architecture Testing** - End-to-end validation

### 3. Change Author & Team Name

To update author/team details, edit:

```
layouts/partials/menu-footer.html
```

### 4. GitHub Actions (CI/CD)

You can automate the build & deploy process with GitHub Actions to deploy to GitHub pages.
Watch this guide for setting up GitHub Actions with Hugo:
📺 [GitHub Actions Setup Video](https://www.youtube.com/watch?v=IlxlD-BWI88)

## 🏗️ Architecture Overview

This workshop demonstrates a serverless architecture pattern using:

- **API Gateway** → **Lambda** → **DynamoDB**
- **SQS** for decoupling and reliability
- **SNS** for notifications and fan-out patterns
- **DynamoDB Streams** for real-time data processing

## 📚 Resources

- [AWS Architecture Center](https://aws.amazon.com/architecture/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Hugo Documentation](https://gohugo.io/documentation/)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

---

**Happy Learning! 🚀**

_Được tạo bởi AWS First Cloud Journey community_
