# 🚀 **Initial Setup for AWS Application Migration Service (MGN)**

## **🔹 Overview**
Before I can start migrating workloads using **AWS Application Migration Service (MGN)**, I need to initialize the service in my AWS account. This involves setting up **IAM Service-Linked Roles** and configuring the **Replication Server template**.

### **🔹 What is a Replication Server?**
Replication servers are lightweight Amazon EC2 instances used to **replicate data** from my source servers to AWS. The **Replication Server template** determines their configuration, including the subnet and security settings.

---

## **📌 Step-by-Step Setup**

### **1️⃣ Initialize AWS MGN**
1. Navigate to **AWS Console → Migration & Transfer → Application Migration Service**.
2. Click **"Get Started"** and then select **"Set up service"**.
3. Wait for initialization to complete.

🔗 **[AWS MGN Setup Guide](https://docs.aws.amazon.com/mgn/latest/ug/getting-started.html)**  

---

### **2️⃣ Customize Replication Server Template**
1. In **AWS MGN Console**, go to **Replication template** in the left-hand menu.
2. Click **Edit** to update the default template.

#### **🔹 Modify Subnet Configuration**
| **Parameter**            | **Value**                  |
|--------------------------|----------------------------|
| Staging area subnet      | `TargetVPC-public-a`       |

3. Click **Save template**.

📌 This ensures that my **Replication Servers** are deployed in the correct **TargetVPC** subnet.

---

### **3️⃣ (Optional) Enable Post-Launch Actions**
Post-launch actions help me automate post-migration configurations. I will enable **AWS Systems Manager Agent (SSM)** so I can execute scripts on migrated instances.

1. In **AWS MGN Console**, navigate to **Post-launch template**.
2. Click **Edit**.
3. Enable **"Install the Systems Manager agent and allow executing actions on launched servers"**.
4. Click **Save template**.

📌 This step is **optional** but recommended to streamline **post-migration automation**.

---

## **🎯 Next Steps**
✅ AWS MGN is now **initialized and configured**!  
➡️ **[Proceed to Deploy AWS MGN Agent](./deploy-mgn-agent.md)**  
