# AWS Three-Tier Architecture using CloudFormation

This project demonstrates the **design and deployment of a highly available, secure, and scalable three-tier architecture on AWS** using **Infrastructure as Code (IaC)** with **AWS CloudFormation**.

The architecture follows **AWS best practices** by separating the application into **Web**, **Application**, and **Database** tiers, deployed across **multiple Availability Zones** for fault tolerance and high availability.

---

## 📌 Project Overview

Modern cloud applications require:

* Scalability
* High availability
* Network isolation
* Secure access control
* Automation

This project focuses on building a **robust networking foundation** that can support production workloads and can be easily extended with compute, database, and monitoring services.

---

## 🏗 Architecture Design

### Three-Tier Architecture

```
Internet
   |
[ Web Tier ]
   |
[ Application Tier ]
   |
[ Database Tier ]
```

### Tier Responsibilities

#### Web Tier (Public)

* Handles user-facing traffic
* Deployed in **public subnets**
* Internet access via **Internet Gateway**
* Protected using **Web Security Group**

#### Application Tier (Private)

* Handles business logic
* Deployed in **private subnets**
* No direct internet access
* Outbound access via **NAT Gateway**
* Accessible only from Web tier

#### Database Tier (Private & Isolated)

* Stores application data
* Deployed in **isolated private subnets**
* No public internet access
* Accessible only from Application tier

---

## 🌐 Network Architecture

* **Custom VPC:** `10.0.0.0/16`
* **Availability Zones:** 2
* **Subnets:**

  * 2 Public subnets (Web tier)
  * 2 Private subnets (Application tier)
  * 2 Private subnets (Database tier)

### Routing Design

* Public subnets route traffic via **Internet Gateway**
* Private subnets route outbound traffic via **NAT Gateway**
* Database subnets remain isolated from the internet

---

## 🔐 Security Design

### Security Groups (Tier-Based Isolation)

| Tier             | Allowed Traffic                    |
| ---------------- | ---------------------------------- |
| Web Tier         | HTTP (80) from Internet            |
| Application Tier | App Port (8080) from Web Tier      |
| Database Tier    | MySQL (3306) from Application Tier |

✔ No public access to Application or Database tiers
✔ Principle of **least privilege** enforced
✔ Clear traffic flow control between tiers

---

## 🧰 AWS Services Used

* Amazon VPC
* Subnets (Public & Private)
* Internet Gateway
* NAT Gateway
* Route Tables
* Elastic IP
* Security Groups
* AWS CloudFormation
* Amazon EC2
* Amazon RDS
* Amazon CloudWatch
* Amazon Route 53
* AWS Certificate Manager (ACM)


---

## 🛠 Infrastructure as Code (IaC)

The entire network infrastructure is provisioned using **AWS CloudFormation**, enabling:

* Repeatable deployments
* Version control
* Easy teardown and recreation
* Reduced human error

---

## 📁 Repository Structure

```
aws-three-tier-architecture-cloudformation/
│
├── cloudformation/
│   └── vpc-network.yaml
│
├── diagrams/
│   └── three-tier-architecture.png
│
├── README.md
├── LICENSE
└── .gitignore
```

---

## 🚀 Deployment Instructions

### Prerequisites

* AWS account
* IAM user with permissions for VPC, EC2, and CloudFormation

### Steps

1. Clone the repository

   ```bash
   https://github.com/sujalkamanna/three-tier-architecture.git
   ```

2. Open AWS Console → **CloudFormation**

3. Click **Create stack → With new resources**

4. Upload the template:

   ```
   cloudformation/vpc-network.yaml
   ```

5. Proceed with default options and deploy

6. Wait for stack status:

   ```
   CREATE_COMPLETE
   ```

---

## 📊 Validation Checklist

After deployment, verify:

* VPC created with correct CIDR
* Subnets distributed across two AZs
* NAT Gateway present in public subnet
* Route tables correctly associated
* No public IPs assigned to private subnets
* Security Groups enforce tier-based access

---

## 🔜 Future Enhancements

This project is designed to be **extended incrementally**:

* Application Load Balancer (ALB)
* Auto Scaling Groups (ASG)
* Amazon EC2 instances
* Amazon RDS (Multi-AZ)
* CloudWatch monitoring and alarms
* Route 53 and ACM for HTTPS
* AWS WAF for security hardening

---

## 🎯 Key Learnings

* Designing AWS network architectures from scratch
* Implementing secure subnet isolation
* Managing internet access using IGW and NAT Gateway
* Writing production-ready CloudFormation templates
* Applying AWS best practices for high availability and security

---

## 👨‍💻 Author

**Sujal Kamanna**
Cloud / DevOps Enthusiast

LinkedIn: 

GitHub: https://github.com/sujalkamanna/

---

## 📄 License

This project is licensed under the **MIT License** — free to use, modify, and distribute.

---

## ⭐ Final Note

This project represents a **real-world cloud networking foundation** and serves as a strong base for deploying scalable applications on AWS.

If you found this useful, feel free to ⭐ the repository!

---
