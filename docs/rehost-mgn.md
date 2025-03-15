# 🚀 **Rehost with AWS Application Migration Service (MGN)**

## **🔹 Overview**
Rehosting, also known as **Lift and Shift**, is one of the fastest migration strategies to move workloads from on-premises to AWS. In this project, I am leveraging **AWS Application Migration Service (MGN)** to migrate a web application from a traditional on-premises setup to AWS with minimal changes.

### **🔹 Why Rehost?**
✅ **Minimal modifications**: No need to rewrite application code.  
✅ **Faster migration**: Quickly lift and shift workloads to AWS.  
✅ **Preserve existing configurations**: Keep OS, applications, and settings intact.  
✅ **Enable future modernization**: Easily replatform or refactor later.  

---

## **📌 Rehosting Process**
This migration follows a **four-step process** using AWS MGN:

### **1️⃣ Configure AWS MGN**
- Set up **AWS Application Migration Service** in the AWS Console.
- Define the **source environment** and **target AWS infrastructure**.

### **2️⃣ Deploy the AWS Replication Agent**
- Install and configure the **AWS Replication Agent** on source servers.
- Verify that continuous data replication is enabled.

### **3️⃣ Launch Test and Cutover Instances**
- Perform a **test migration** to validate application functionality.
- When ready, **cutover to AWS** for final migration.

### **4️⃣ Decommission and Optimize**
- Decommission the **on-premises environment**.
- Optimize resources for **cost efficiency**.

---

## **📌 Step-by-Step Implementation**
### **1️⃣ Configure AWS MGN**
1. Navigate to **AWS Console → Migration & Transfer → AWS Application Migration Service (MGN)**.
2. Click **"Get started"** and configure **Source Servers**.
3. Define the **Replication Settings**:
   - **Target Subnet**: Choose the appropriate **TargetVPC**.
   - **Instance Type**: Select instance types for replicated instances.
   - **IAM Role**: Ensure the required permissions are in place.

🔗 **[AWS MGN Setup Guide](https://docs.aws.amazon.com/mgn/latest/ug/getting-started.html)**  

---

### **2️⃣ Deploy the AWS Replication Agent**
1. **Install the AWS Replication Agent** on source servers:
   ```bash
   curl -o ./aws-replication-installer.sh https://aws-replication-agent.s3.amazonaws.com/latest/aws-replication-installer.sh
   sudo bash aws-replication-installer.sh
   ```   
2.Register the source server with AWS MGN:
```bash
sudo mgn-cli register --aws-access-key <AWS_ACCESS_KEY> --aws-secret-key <AWS_SECRET_KEY> --region us-west-2
```
3.Verify replication status in AWS MGN Console.

### **3️⃣ Launch Test and Cutover Instances**
🔹 Perform a Test Migration
In AWS MGN Console, select Test Instance.
Launch the instance in a test environment.
Validate networking, performance, and application functionality.
🔹 Final Cutover to AWS
Choose Launch Cutover Instance.
Once running, verify data integrity and system performance.
If everything looks good, finalize the cutover.

### **4️⃣ Decommission and Optimize**
✅ Terminate source instances once AWS migration is complete.

✅ Update DNS records to point to AWS-hosted applications.

✅ Enable AWS Auto Scaling for better performance.

✅ Implement AWS Cost Optimization best practices.

🎯 Next Steps
Now that the application is successfully migrated, it's time to Replatform for Optimization!
🔜 Proceed to Replatforming with Amazon ECS
