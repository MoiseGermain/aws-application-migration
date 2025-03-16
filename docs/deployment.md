# **Application Migration to AWS**
### **Deploying a Scalable Cloud Environment**

In this project, I designed and deployed a **production-ready AWS environment** to migrate a web application. The infrastructure is automated using **AWS CloudFormation**, ensuring consistency, security, and scalability. 

## **📌 Infrastructure Overview**
The deployment includes:
- **Two EC2 instances (`t3.micro`)**:  
  - **Web Server** – Hosts the application.  
  - **Database Server** – Stores application data.
- **NAT Gateway** – Enables secure outbound internet access for private resources.
- **API Gateway** – Manages API access securely.
- **AWS Lambda Functions** – Automates EC2 access key retrieval.

This setup ensures **high availability, security, and operational efficiency** for running cloud-based applications.

---

## **🚀 Deployment Using AWS CloudFormation**
Since I wanted to automate the provisioning of this infrastructure, I used **AWS CloudFormation** to define and deploy the resources. This method eliminates manual configurations, reduces errors, and ensures best practices.

### **Step 1: Launch CloudFormation Stack**
To deploy the infrastructure, click the link below to launch the **CloudFormation stack**:  
👉 **[Deploy AWS Infrastructure](https://ws-assets-prod-iad-r-pdx-f3b3f9f1a7d6a3d0.s3.us-west-2.amazonaws.com/c6bdf8dc-d2b2-4dbd-b673-90836e954745/migration_workshop_source_template.yml)**  

---

### **Step 2: Configure the CloudFormation Stack**
1. **Specify CloudFormation Template**
   - Ensure the **Amazon S3 URL** field contains:
     ```
     https://ws-assets-prod-iad-r-pdx-f3b3f9f1a7d6a3d0.s3.us-west-2.amazonaws.com/c6bdf8dc-d2b2-4dbd-b673-90836e954745/migration_workshop_source_template.yml
     ```
   - Click **Next**.

2. **Define Stack Details**
   - Set **Stack Name** to:
     ```
     ApplicationMigrationDeployment
     ```
   - Click **Next**.

3. **Configure Stack Options**
   - No changes are needed. Click **Next**.

4. **Review and Deploy**
   - Scroll down and **check all required IAM permissions checkboxes**.
   - Click **Create Stack**.

---

### **Step 3: Verify Deployment**
Once the deployment begins, I monitor the process and verify the resources were created successfully.

1. **Monitor Deployment Progress**  
   - Navigate to **AWS Console → CloudFormation**.
   - Locate the **ApplicationMigrationDeployment** stack.
   - Wait for the status to change to **CREATE_COMPLETE**.

2. **Retrieve Deployment Details**  
   - In the **CloudFormation Console**, select **ApplicationMigrationDeployment**.
   - Go to the **Outputs** tab.
   - Copy the generated **EC2 instance details, NAT Gateway, API Gateway endpoints, and Lambda function outputs** for future reference.

---

## **🛠 Troubleshooting Deployment Issues**
While deploying, I accounted for potential errors and found solutions to common issues:
- **Check the "Events" tab** in CloudFormation to diagnose failures.
- **Common issue**: Pre-existing IAM roles (`ecsExecutionRole`, `ecsAutoscaleRole`) may cause conflicts.
  - **Solution**: Delete these roles and re-run the deployment.
  - If these roles are required for other applications, modifying the IAM policy in CloudFormation before re-deployment is an alternative fix.

---

## **✅ Next Steps**
➡️ **[Review the Deployed Infrastructure](../docs/review-deployment.md)**  
➡️ **[Begin Application Migration](../docs/migration.md)**  
➡️ **[Troubleshoot Deployment Issues](../docs/troubleshooting.md)**  

This project demonstrates how I successfully **migrated an application to AWS**, using **CloudFormation** to create a **scalable, secure, and automated cloud environment** for production workloads.
