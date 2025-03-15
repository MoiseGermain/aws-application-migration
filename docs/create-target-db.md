# 🏗️ **Create Target Database (Amazon RDS MySQL)**

## **Overview**
To perform **continuous data replication** using **AWS Database Migration Service (DMS)**, I first need to **set up a target database**. I will use **Amazon Relational Database Service (Amazon RDS)**, which provides a **fully managed** database service.

The steps in this section:
- **Create a DB Subnet Group** (to control where Amazon RDS will be deployed).
- **Create the Amazon RDS MySQL Instance** (as the target database).

---

## **🔹 Step 1: Create the Subnet Group for Target Database**
The **DB Subnet Group** allows me to **define the subnets** where my **RDS instance** will be deployed.

### **1️⃣ Navigate to AWS RDS Subnet Groups**
1. Open **AWS Console** → **Services** → **Database** → **RDS**.
2. Select **Subnet Groups** from the left menu.
3. Click **Create DB subnet group**.

🔗 **[AWS RDS Subnet Groups](../assets/rds-subnet-groups.png)**

### **2️⃣ Configure the DB Subnet Group**
| Parameter | Value |
|-----------|----------------------------|
| **Name** | `database-subnet-group` |
| **Description** | Subnets where RDS will be deployed |
| **VPC** | `TargetVPC` |
| **Availability Zones** | Select `us-west-2a` and `us-west-2b` |
| **Add subnets** | Add `10.0.101.0/24`, `10.0.201.0/24` |

🔗 **[DB Subnet Group Configuration](../assets/db-subnet-group-config.png)**

Click **Create**.

---

## **🔹 Step 2: Create the Target Database**
Now, I will create a **MySQL database instance** using **Amazon RDS**.

### **1️⃣ Navigate to AWS RDS Databases**
1. In the **AWS Console**, go to **RDS**.
2. Click **Databases** on the left menu.
3. Click **Create database**.

🔗 **[AWS RDS Database Creation](../assets/rds-create-db.png)**

---

### **2️⃣ Configure the Database Engine**
| Parameter | Value |
|-----------|----------------------------|
| **Engine type** | MySQL |
| **Engine version** | Newest from **5.7** family |

🔗 **[RDS Engine Selection](../assets/rds-engine-selection.png)**

---

### **3️⃣ Select Free Tier**
For cost optimization, I will use **Free Tier**:

🔗 **[Free Tier Selection](../assets/rds-free-tier.png)**

Since Free Tier is selected, **Single DB instance** is automatically chosen for availability and durability.

🔗 **[Availability & Durability Settings](../assets/rds-availability.png)**

---

### **4️⃣ Set Up Database Credentials**
| Parameter | Value |
|-----------|----------------------------|
| **DB instance identifier** | `database-1` |
| **Master username** | `admin` |
| **Master password** | `VeryHardPassword` |

🔗 **[RDS Credentials Setup](../assets/rds-credentials.png)**

⚠️ **Note:** The **password above is not secure** and should not be used in a real production environment.

---

### **5️⃣ Configure Instance Settings**
| Parameter | Value |
|-----------|----------------------------|
| **Instance class** | `db.t3.micro` (Burstable DB instance) |

🔗 **[RDS Instance Configuration](../assets/rds-instance-config.png)**

---

### **6️⃣ Configure Storage**
| Parameter | Value |
|-----------|----------------------------|
| **Storage type** | `General Purpose SSD (gp3)` |
| **Allocated storage** | `20 GB` |
| **Enable storage autoscaling** | ❌ Unchecked |

🔗 **[RDS Storage Configuration](../assets/rds-storage.png)**

---

### **7️⃣ Configure Connectivity**
| Parameter | Value |
|-----------|----------------------------|
| **Virtual private cloud (VPC)** | `TargetVPC` |
| **DB subnet group** | `database-subnet-group` |
| **VPC security group (firewall)** | `Choose Existing` |
| **Existing VPC security groups** | Select **DB-SG** only |

🔗 **[RDS Connectivity Settings](../assets/rds-connectivity.png)**

---

### **8️⃣ Disable Unnecessary Features**
- **Database Authentication:** `Password authentication`  
- **Monitoring:** `Disable Enhanced Monitoring`  
- **Backups & Auto Upgrades:** `Disable automated backups` and `auto minor version upgrade`  

🔗 **[RDS Backup & Monitoring Settings](../assets/rds-backup-monitoring.png)**

---

### **9️⃣ Review & Create Database**
1. **Review the estimated monthly cost.**
2. Click **Create database**.

🔗 **[RDS Cost Estimation](../assets/rds-costs.png)**

---

## **✅ Final Step: Verify Database Status**
The **RDS Database Instance** creation will take a few minutes. I will **monitor the status** in **RDS → Databases** until it shows **Available**.

🔗 **[RDS Instance Available](../assets/rds-instance-available.png)**

---

## **🎯 Next Steps**
➡️ **[Set Up AWS DMS Replication Instance](./create-replication-instance.md)**
