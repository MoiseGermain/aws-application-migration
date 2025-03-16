# **🚀 Deploy an AWS Application Load Balancer (ALB)**

## **📌 Overview**
To handle incoming traffic efficiently, I will create an **Application Load Balancer (ALB)** in AWS.  
This ALB will distribute traffic across ECS tasks running my **WordPress containerized application**.

✅ **Balance traffic for high availability**  
✅ **Ensure fault tolerance and scalability**  
✅ **Secure traffic routing with target groups**  

---

## **🛠️ Step 1: Create a Target Group**
📌 **The target group will register ECS tasks and direct traffic from the ALB.**

1️⃣ In **AWS Console**, go to **Services > EC2 > Target Groups**  
2️⃣ Click **Create target group**  
3️⃣ Enter the following details:  

| Parameter            | Value                          |
|----------------------|--------------------------------|
| **Target type**      | `IP addresses` (for ECS tasks) |
| **Name**            | `ecs-target-group`             |
| **VPC**             | `TargetVPC`                    |

📷 [**Create EC2 Target Group**](images/create-target-group.png)

4️⃣ Click **Next**  
5️⃣ On **Register targets**, leave everything as default  
6️⃣ Click **Create target group**  

✅ **Target group is now ready for use with the ALB.**

---

## **🛠️ Step 2: Create an Application Load Balancer (ALB)**
📌 **Now, I will create an ALB that routes traffic to my target group.**

1️⃣ In **AWS Console**, go to **Services > EC2 > Load Balancers**  
2️⃣ Click **Create Load Balancer**  
3️⃣ Select **Application Load Balancer**  
4️⃣ Click **Create**  

📷 [**Create an ALB**](images/create-alb.png)

---

## **🛠️ Step 3: Configure the Load Balancer**
📌 **Enter basic ALB settings.**  

| Parameter            | Value                          |
|----------------------|--------------------------------|
| **Name**            | `ecs-alb`                      |
| **Scheme**          | `Internet-facing`              |
| **IP Address Type** | `IPv4`                         |

📷 [**Configure ALB Basic Settings**](images/configure-alb.png)

Click **Next**.

---

## **🛠️ Step 4: Configure Network Mapping**
📌 **Select the VPC and public subnets for high availability.**  

| Parameter       | Value                |
|---------------|--------------------|
| **VPC**       | `TargetVPC`        |
| **Subnets**   | `Public Subnet A, Public Subnet B` |

📷 [**Select VPC and Public Subnets**](images/select-vpc-subnets.png)

Click **Next**.

---

## **🛠️ Step 5: Configure Security Groups**
📌 **Assign the previously created security group to the ALB.**  

1️⃣ Select **LB-SG** from the list  
2️⃣ Click **Next**  

📷 [**Select LB-SG Security Group**](images/select-lb-sg.png)

---

## **🛠️ Step 6: Configure Listeners and Target Group**
📌 **The ALB listener will direct traffic to the ECS target group.**  

| Parameter                | Value                     |
|--------------------------|--------------------------|
| **Listener Protocol**    | `HTTP (80)`              |
| **Forward to**           | `ecs-target-group`       |

📷 [**Configure ALB Listener**](images/configure-listener.png)

Click **Next**, then **Create Load Balancer**.

✅ **ALB is now successfully deployed.**

---

## **📌 Next Steps**
➡️ **Step 5: [Deploy an ECS Cluster](./create-ecs-cluster.md)**
