# 🚀 **Create AWS DMS Replication Instance**

## **Overview**
Now that I have the **target database ready**, it's time to **set up AWS Database Migration Service (DMS)**. A key component is the **Replication Instance**, which is a managed **Amazon EC2 instance** that hosts **replication tasks**.

- A **single replication instance** can manage **multiple replication tasks**.
- The **DMS Replication Instance** will connect to both the **source** and **target databases**.

🔗 **[AWS DMS Overview](../assets/dms-overview.png)**

---

## **🔹 Step 1: Create Replication Subnet Group**
Similar to the **Target DB Instance**, the **DMS Replication Instance** also needs a **Subnet Group**.

### **1️⃣ Navigate to AWS DMS Subnet Groups**
1. Open **AWS Console** → **Services** → **Migration & Transfer** → **Database Migration Service**.
2. Select **Subnet Groups** from the left menu.
3. Click **Create subnet group**.

🔗 **[AWS DMS Subnet Groups](../assets/dms-subnet-groups.png)**

### **2️⃣ Configure the Subnet Group**
| Parameter | Value |
|-----------|----------------------------|
| **Name** | `dms-subnet-group` |
| **Description** | Default VPC Subnet Group for DMS |
| **VPC** | `TargetVPC` |
| **Add subnets** | `TargetVPC-public-a`, `TargetVPC-public-b` |

🔗 **[DMS Subnet Group Configuration](../assets/dms-subnet-group-config.png)**

Click **Create subnet group**.

---

## **🔹 Step 2: Create AWS DMS Replication Instance**
Now, I will **create the AWS DMS Replication Instance**, which will handle the **data migration**.

### **1️⃣ Navigate to AWS DMS Replication Instances**
1. Open **AWS Console** → **Services** → **Migration & Transfer** → **Database Migration Service**.
2. Select **Replication instances** from the left menu.
3. Click **Create replication instance**.

🔗 **[AWS DMS Replication Instances](../assets/dms-replication-instance.png)**

---

### **2️⃣ Configure the Replication Instance**
| Parameter | Value |
|-----------|----------------------------|
| **Name** | `replication-instance` |
| **Description** | DMS replication instance |
| **Instance class** | `dms.t3.medium` |
| **Multi-AZ Deployment** | ❌ `Dev or test workload (Single-AZ)` |

🔗 **[DMS Replication Instance Configuration](../assets/dms-instance-config.png)**

---

### **3️⃣ Configure Connectivity**
| Parameter | Value |
|-----------|----------------------------|
| **Replication subnet group** | `dms-subnet-group` |
| **Availability Zone** | `us-west-2a` |
| **VPC Security Group** | Select the **replication instance security group** created earlier |

🔗 **[DMS Replication Instance Connectivity](../assets/dms-instance-connectivity.png)**

Click **Create**.

📌 **Note:** It may take **10-15 minutes** for the **DMS Replication Instance** to reach **Available** status.

---

## **🔹 Step 3: Modify Source DB Security Group**
Since the **source database** is in a **different VPC**, I need to **allow access** from the **DMS Replication Instance**.

### **1️⃣ Retrieve Public IP of Replication Instance**
Once the **Replication Instance** is created, note its **public IP address**.

🔗 **[DMS Replication Instance Public IP](../assets/dms-public-ip.png)**

---

### **2️⃣ Modify Security Group of Source Database**
1. Open **AWS Console** → **Services** → **Compute** → **EC2**.
2. Select **Security Groups**.
3. Locate **DB-SG** (the security group assigned to the source database).
4. Click **Edit inbound rules**.

🔗 **[Modify Source DB Security Group](../assets/dms-edit-db-sg.png)**

---

### **3️⃣ Add an Inbound Rule**
| Parameter | Value |
|-----------|--------------------------------|
| **Type** | `MYSQL/Aurora` |
| **Source** | `Public IP address of DMS Replication Instance` |

🔗 **[DMS Inbound Rule for Source DB](../assets/dms-inbound-rule.png)**

Click **Save rule**.

📌 **Note:** In a **real-world scenario**, this **communication would be private** or protected by **VPN / Direct Connect**.

---

## **✅ Final Step: Verify Replication Instance**
1. Go to **AWS Console** → **DMS** → **Replication Instances**.
2. Wait until **Status** changes to **Available**.


---

## **🎯 Next Steps**
➡️ **[Configure Source Database](./configure-source-db.md)**
