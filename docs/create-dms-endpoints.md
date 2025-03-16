# 🔗 **Create Source and Target Endpoints for AWS DMS**

## **Overview**
AWS DMS **uses endpoints** to access the **source and target databases** before executing **replication tasks**. In this section, I will configure:
✔️ **Source Endpoint** → MySQL database running on **Source-DBServer (EC2)**
✔️ **Target Endpoint** → MySQL database running on **Amazon RDS**

🔹 **Reminder**  
If my **DMS Replication Instance** is still not **Available**, I may need to **configure the Source DB's Security Group** before proceeding.

---

## **🔹 Step 1: Create Source Endpoint**
### **1️⃣ Navigate to AWS DMS**
1. **Open AWS Console** → **Services** → **Migration & Transfer** → **Database Migration Service**.
2. Select **Endpoints** from the left-hand menu.
3. Click **Create endpoint**.

🔗 **[AWS DMS Endpoints Console](assets/aws-dms-endpoints.png)**

---

### **2️⃣ Fill in the Endpoint Configuration**
| **Parameter**              | **Value** |
|---------------------------|-----------|
| **Endpoint Type**          | Source Endpoint |
| **Endpoint Identifier**    | `source-endpoint` |
| **Descriptive ARN**        | (Keep default: Empty) |
| **Source Engine**          | MySQL |
| **Access to Database**     | Provide access information manually |
| **Server Name**            | Use **`DBServerDNSName`** from the **CloudFormation Outputs** |
| **Port**                   | `3306` |
| **User Name**              | `wordpress-user` |
| **Password**               | `AWSRocksSince2006` |
| **SSL Mode**               | (Keep default: none) |

---

### **3️⃣ Test Source Endpoint Connection**
Before clicking **Create endpoint**, I will:
1. Expand **Test endpoint connection (optional)**.
2. Ensure **TargetVPC** and **DMS Replication Instance** are prepopulated.
3. Click **Run test**.

📌 **Expected Outcome** → ✅ **Successful Connection**  
🔗 **[Test Endpoint Success](assets/dms-test-endpoint.png)**

📌 **If test fails**, I will check:
✔️ The **endpoint parameters** (server name, username, password).  
✔️ The **Source DB Security Group** allowing **DMS RI access**.  
✔️ The **DMS Replication Instance** is **publicly accessible**.

---

## **🔹 Step 2: Create Target Endpoint**
Now, I will **repeat the process** to create the **Target Endpoint**.

### **1️⃣ Fill in the Target Endpoint Configuration**
| **Parameter**              | **Value** |
|---------------------------|-----------|
| **Endpoint Type**          | Target Endpoint |
| **RDS Instance**           | Select **MySQL RDS Instance** from the drop-down |
| **Endpoint Identifier**    | `target-endpoint` |
| **Descriptive ARN**        | (Keep default: Empty) |
| **Target Engine**          | MySQL (pre-populated) |
| **Access to Database**     | Provide access information manually |
| **Server Name**            | DNS Name of **Amazon RDS Instance** (pre-populated) |
| **Port**                   | `3306` (pre-populated) |
| **SSL Mode**               | (Keep default: none) |
| **User Name**              | `admin` (pre-populated) |
| **Password**               | Enter password used for RDS creation (Default: `VeryHardPassword`) |

---

### **2️⃣ Test Target Endpoint Connection**
Before clicking **Create endpoint**, I will:
1. Expand **Test endpoint connection (optional)**.
2. Ensure **TargetVPC** and **DMS Replication Instance** are prepopulated.
3. Click **Run test**.

📌 **Expected Outcome** → ✅ **Successful Connection**  
🔗 **[Test Endpoint Success](assets/dms-test-endpoint.png)**

📌 **If test fails**, I will check:
✔️ The **endpoint parameters** (server name, username, password).  
✔️ The **Target DB Security Group** allowing **DMS RI access**.

---

## **🎯 Next Steps**
✅ Now that I have successfully configured the **DMS Endpoints**, I can proceed with:
➡️ **[Create and Run Replication Task](./create-replication-task.md)** 🚀
