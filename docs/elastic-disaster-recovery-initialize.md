# **🔹 Initializing AWS Elastic Disaster Recovery (EDR) Service**

## **📌 Overview**
Before using **AWS Elastic Disaster Recovery (EDR)**, I need to initialize the service in the **Disaster Recovery (DR) AWS Region** (`us-west-1`). This one-time initialization process will:
✅ **Create default replication settings**  
✅ **Generate IAM roles required for EDR**  
✅ **Enable server replication and recovery**  

📌 **Ensure that the AWS Region is set to `N. California (us-west-1)` before proceeding.**  

---

## **📍 Step 1: Open the AWS Elastic Disaster Recovery Console**
1️⃣ In the **AWS Console**, go to:  
   **Services → AWS Elastic Disaster Recovery**  
2️⃣ Click **Configure and initialize** on the landing page.  

📷 **[EDR Initialization](images/edr-init.png)**  

---

## **📍 Step 2: Configure AWS Elastic Disaster Recovery**
### **🔹 Step 2.1: Setup Replication Server Details**
1️⃣ In **Step 1: Setup replication server details**, go to **Replication server configuration**.  
2️⃣ Change the **Staging area subnet** to:  
   ➝ `Elastic-DR-subnet-us-west-1a`  
3️⃣ Click **Next**.  

📷 **[Replication Server Configuration](images/step1-replication-server-config.png)**  

---

### **🔹 Step 2.2: Specify Volumes and Security Groups**
1️⃣ In **Step 2: Specify volumes and security groups**, leave everything as default.  
2️⃣ Click **Next**.  

---

### **🔹 Step 2.3: Configure Additional Replication Settings**
1️⃣ In **Step 3: Configure additional replication settings**, leave everything as default.  
2️⃣ Click **Next**.  

---

### **🔹 Step 2.4: Set Default DRS Launch Settings**
1️⃣ In **Step 4: Set default DRS launch settings**, go to **Automated launch settings**.  
2️⃣ Select **Inactive** (we will specify the instance type later in the launch template).  
3️⃣ Click **Next**.  

📷 **[DRS Launch Settings](images/step4-replication-launch-settings.png)**  

---

### **🔹 Step 2.5: Set Default EC2 Launch Template**
1️⃣ In **Step 5: Set default EC2 launch template**, configure:

| **Parameter**         | **Value**                                      |
|-----------------------|-----------------------------------------------|
| **Subnet**           | `Elastic-DR-subnet-public2-us-west-1c` |
| **Security Groups**   | `DR-WebserverSG` |
| **Instance Type**     | `t3.small` |
| **EBS Volume Type**   | `General Purpose SSD (gp3)` |

2️⃣ Expand the **Advanced settings** section.  
3️⃣ Select **IAM instance profile**:  
   ➝ `migration-workshop-source-template-EC2InstanceProfile-xxx`  
4️⃣ Click **Next**.  

📷 **[EC2 Launch Template Configuration](images/step5-ec2-launch-settings.png)**  

---

## **📍 Step 3: Finalize Initialization**
1️⃣ In **Step 6: Review and initialize**, review all settings.  
2️⃣ Click **Configure and initialize** to complete the setup.  

---

## **🚀 Next Steps**
Now that **AWS Elastic Disaster Recovery (EDR) is initialized**, I will proceed with:  
➡️ **Installing the AWS replication agent on the source servers.**  

📌 **[Proceed to Next Step: Installing AWS Replication Agent](./elastic-disaster-recovery-replication.md)**  
