# **Review Deployed Environment**

## **Overview**
This project demonstrates a **real-world AWS migration strategy**, showcasing the transition of an **on-premises** workload to AWS. It follows best practices for **scalability, security, and high availability**, leveraging AWS **Application Migration Service (MGN), AWS Database Migration Service (DMS), Amazon ECS, and Elastic Beanstalk**.

The **source environment** mimics an **on-premises data center**, while the **target environment** is designed to be **production-ready**, following AWS **Landing Zone principles**.

---

## **Source Environment**
In a typical migration scenario, workloads originate from **on-premises virtualized environments**. For this project, the source environment is **simulated in AWS** within a **dedicated VPC (`SourceVPC`)**, mimicking an **on-prem** setup.

### **Source Workload Components**
- **Application Server (`Source-Webserver`)**
  - Hosts an **eCommerce Web Application** (WordPress + WooCommerce)
  - Runs on **PHP 7.x**
  - Deployed on **Amazon Linux**

- **Database Server (`Source-DBServer`)**
  - Uses **self-managed MySQL 5.7.x**
  - Runs on **Amazon Linux**

### **Accessing the Source Application**
The deployed application can be accessed via **WebServerDNSName**, which can be retrieved from **AWS CloudFormation Outputs**.  
To test accessibility:
1. Navigate to **AWS Console → CloudFormation → ApplicationMigrationStack → Outputs**
2. Locate `WebServerDNSName`
3. Open a web browser and enter the DNS name over **HTTP**  
   - Expected Result: The sample **eCommerce website** should load successfully.

---

## **Target Environment**
A **well-architected migration** involves transitioning workloads into a **secure, scalable, and highly available AWS environment**.  
For this project, the **target environment (`TargetVPC`)** follows AWS **Landing Zone architecture**.

### **TargetVPC Configuration**
✅ **Multi-AZ Deployment** – Ensures high availability  
✅ **Private Subnets** – Used for application and database tiers  
✅ **Security Groups & IAM Roles** – Implement least privilege access  
✅ **Scalable & Resilient Infrastructure** – Supports modern application architectures  

### **Current Target Environment State**
The **TargetVPC** is currently **provisioned** but remains **empty**. As the migration progresses, workloads will be deployed into this environment based on the chosen **migration strategy**.

---

## **Next Steps**
➡️ **[Deploy the Migration Strategy](../docs/deployment.md)**  
➡️ **[Troubleshoot Issues](../docs/troubleshooting.md)**  

---

## **Project Summary**
This project provides **hands-on experience** with **AWS migration services**, simulating the migration of a real-world application. The following AWS services are utilized:  

🔹 **AWS Application Migration Service (MGN)** – Rehosting workloads  
🔹 **AWS Database Migration Service (DMS)** – Replatforming databases  
🔹 **Amazon ECS & Elastic Beanstalk** – Modernizing application deployments  
🔹 **AWS Elastic Disaster Recovery (EDR)** – Ensuring business continuity  

This structured approach **demonstrates best practices** for migrating and modernizing applications on AWS.

---

