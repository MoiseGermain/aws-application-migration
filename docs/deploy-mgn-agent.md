# 🚀 **Installing AWS MGN Replication Agent**

## **🔹 Overview**
AWS Application Migration Service (MGN) **rehosts** servers to AWS by replicating **block-level data** from the source environment to the cloud. This can be done **agent-based** or **agentless**.  
For my migration, I will use the **agent-based** replication, which is **recommended** for most use cases.

### **🔹 How the MGN Agent Works**
- The **AWS Replication Agent** performs an **initial block-level read** of any volume attached to my source server.
- It then **replicates** that data to a **replication server** in AWS.
- Any **subsequent writes** or modifications are **captured** and **synchronized** continuously, ensuring **near-zero RPO (Recovery Point Objective).**

---

## **📌 Step-by-Step Installation**

### **1️⃣ Retrieve IAM Credentials for MGN Agent**
Before I install the **AWS Replication Agent**, I need IAM credentials with **proper permissions** to communicate with AWS MGN APIs.  
These credentials are already created and available in my IAM Console.

📌 **AWS MGN also supports using temporary credentials via IAM Roles Anywhere.** If preferred, I can refer to the **[MGN documentation](https://docs.aws.amazon.com/mgn/latest/ug/credentials.html)** for more details.

---

### **2️⃣ Connect to the Source Server**
1. **Navigate to AWS Console** → Services → **Compute** → **EC2**.
2. Click **Instances** on the left menu.
3. Select the instance named **`Source-Webserver`**.
4. Click **Connect** at the top right.
5. Select **Session Manager** tab → Click **Connect**.

🔗 **[AWS EC2 Session Manager Guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html)**  

📌 **Alternative:** I can also connect using **SSH** or **EC2 Instance Connect**, but I must ensure my Security Group rules allow access.

---

### **3️⃣ Download and Install the MGN Agent**
📌 Now, I will **download** the AWS Replication Agent **installation script** and run it.

#### **🔹 Run the following commands in the terminal:**
```bash
cd ~
wget -O ./aws-replication-installer-init.py https://aws-application-migration-service-us-west-2.s3.amazonaws.com/latest/linux/aws-replication-installer-init.py
sudo python3 aws-replication-installer-init.py
```
4️⃣ Enter Required Parameters
During installation, I will be prompted to enter the following values:

Parameter	Value
AWS Region Name	us-west-2
AWS Access Key ID	(Enter AppMigServiceAccessKey from IAM Console)
AWS Secret Access Key	(Enter AppMigServiceSecretAccessKey from IAM Console)
To replicate all disks, press Enter	(Press Enter – I want to replicate all disks)

📌 The MGN Agent installation can take 5-10 minutes to complete.

5️⃣ Verify Replication Status
Once the installation is complete, I can verify that replication is in progress:

Go to AWS Console → Migration & Transfer → Application Migration Service.
I should land on the Source Servers page.
My source server should now be in initial synchronization.
🔗 AWS MGN Source Servers Console

📌 The replication process starts immediately and can take a few minutes to complete.

🎯 Next Steps
➡️ **[Updating Server Details in AWS MGN](./update-server-details.md)**
