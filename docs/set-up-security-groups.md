# **🔒 Set Up Security Groups for Amazon ECS Deployment**

## **📌 Overview**
To ensure secure communication between different AWS services in my ECS setup, I need to create and configure the following security groups:

✅ **Load Balancer Security Group** → Allows public access to the website  
✅ **ECS Tasks Security Group** → Enables communication between the Load Balancer and ECS tasks  
✅ **Elastic File System (EFS) Security Group** → Manages access between ECS tasks and the EFS storage  
✅ **Modify Database Security Group** → Allows ECS tasks to connect to the database  

---

## **🛠️ Step 1: Create Load Balancer Security Group**
📌 **This security group will allow users to access the application through HTTP and HTTPS.**

1️⃣ In the **AWS Console**, go to **Services > Networking & Content Delivery > VPC**  
2️⃣ In the left panel, select **Security Groups**  
3️⃣ Click **Create Security Group**  
4️⃣ Enter the following values:

| Parameter  | Value  |
|------------|--------|
| **Security group name** | `LB-SG` |
| **Description** | `Load balancer security group` |
| **VPC** | `TargetVPC` |

5️⃣ Scroll down to **Inbound rules** and add the following:

| Type   | Protocol | Source         |
|--------|---------|---------------|
| HTTP   | TCP     | Anywhere IPv4 |
| HTTPS  | TCP     | Anywhere IPv4 |

6️⃣ Click **Create security group**  

📷 [**Configure Load Balancer Security Group**](./images/lb-sg-setup.png)

---

## **🛠️ Step 2: Create ECS Tasks Security Group**
📌 **This security group allows communication between the Load Balancer and ECS tasks.**

1️⃣ Go to the **Security Groups** screen and click **Create Security Group**  
2️⃣ Enter the following values:

| Parameter  | Value  |
|------------|--------|
| **Security group name** | `ECS-Tasks-SG` |
| **Description** | `Allow communication between the LB and ECS tasks` |
| **VPC** | `TargetVPC` |

3️⃣ Scroll down to **Inbound rules** and add:

| Type   | Protocol | Source       |
|--------|---------|-------------|
| All TCP | TCP     | Custom > `LB-SG` |

4️⃣ Click **Create security group**  

📷 [**Edit ECS Tasks Security Group**](./images/ecs-tasks-sg.png)

---

## **🛠️ Step 3: Create Elastic File System (EFS) Security Group**
📌 **This security group manages access between ECS tasks and the Amazon EFS file system.**

1️⃣ Go to the **Security Groups** screen and click **Create Security Group**  
2️⃣ Enter the following values:

| Parameter  | Value  |
|------------|--------|
| **Security group name** | `EFS-SG` |
| **Description** | `Allow communication between ECS tasks and EFS` |
| **VPC** | `TargetVPC` |

3️⃣ Scroll down to **Inbound rules** and add:

| Type | Protocol | Source |
|------|---------|--------|
| NFS  | TCP     | Custom > `ECS-Tasks-SG` |
| NFS  | TCP     | Custom > **Security Group of the migrated webserver** |

4️⃣ Click **Create security group**  

📷 [**Create and Configure EFS Security Group**](./images/efs-sg-setup.png)

---

## **🛠️ Step 4: Modify Database Security Group**
📌 **I need to allow ECS tasks to connect to the database.**

1️⃣ In the **AWS Console**, navigate to **Security Groups**  
2️⃣ Select **DB-SG** (the existing database security group)  
3️⃣ Click **Edit inbound rules**  
4️⃣ Add the following inbound rule:

| Type  | Protocol | Source        |
|-------|---------|--------------|
| MySQL | TCP     | Custom > `ECS-Tasks-SG` |

5️⃣ Click **Save rules**  

📷 [**Update Database Security Group**](./images/update-db-sg.png)

---

## **📌 Next Steps**
✅ **Security groups are now configured for my ECS deployment.**  
➡️ **Step 2: [Create Amazon EFS](./create-efs.md)**  
