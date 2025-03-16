# **🚀 Create an Amazon ECS Cluster**

## **📌 Overview**
To run my **WordPress application in containers**, I need to create an **Amazon ECS Cluster** using **AWS Fargate**.

✅ **Provision an ECS Cluster for containerized applications**  
✅ **Use AWS Fargate for serverless container management**  
✅ **Enable CloudWatch for container monitoring**  

---

## **🛠️ Step 1: Create an ECS Cluster**
📌 **Follow these steps to create an ECS cluster.**  

1️⃣ In **AWS Console**, go to **Services > ECS > Clusters**  
2️⃣ Click **Create Cluster**  
3️⃣ Enter the following details:  

| Parameter         | Value                        |
|------------------|----------------------------|
| **Cluster name** | `unicorn-cluster`          |
| **VPC**          | `TargetVPC`                |
| **Subnets**      | `TargetVPC-private-a-web`  |
|                  | `TargetVPC-private-b-web`  |

📷 [**Create ECS Cluster**](./images/create-ecs-cluster.png)

---

## **🛠️ Step 2: Configure Infrastructure**
📌 **Ensure AWS Fargate is selected as the compute option.**  

✅ Keep **AWS Fargate** as the selected option  
✅ Check **Use Container Insights** (to enable CloudWatch metrics)  

Click **Create**.

---

✅ **ECS Cluster is now successfully deployed.**

---

## **📌 Next Steps**
➡️ **Step 6: [Define an ECS Task](./define-ecs-task.md)**
