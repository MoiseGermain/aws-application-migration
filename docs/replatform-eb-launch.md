# **🚀 Launch AWS Elastic Beanstalk Environment**

## **📌 Overview**
In this step, I will:
✅ Create an **Elastic Beanstalk Application**  
✅ Deploy my **WordPress application**  
✅ Configure **Networking, Scaling, and Database connectivity**  

This will fully launch my application on **AWS Elastic Beanstalk**, making it accessible via a Load Balancer.

---

## **🛠️ Step 1: Create Elastic Beanstalk Environment**
### **🔹 Open Elastic Beanstalk Console**
1. Open **AWS Console** and navigate to **Elastic Beanstalk**:  
   [🔗 AWS Elastic Beanstalk Console](https://console.aws.amazon.com/elasticbeanstalk/)
2. Click **Create Application**.

📷 [**Create Elastic Beanstalk Application Screenshot**](./images/create-eb-app.png)

---

### **🔹 Step 2: Configure Application Information**
1. Update **Application and Platform settings** as follows:
   
   | Parameter          | Value |
   |--------------------|------------------------------|
   | **Application Name** | `my-eb-app` |
   | **Platform**        | `PHP` |
   | **Platform Branch** | `PHP 8.1 running on 64-bit Amazon Linux 2` |
   | **Platform Version** | Choose **Recommended Option** (e.g., `3.6.0`) |

📷 [**Elastic Beanstalk Application Settings Screenshot**](./images/eb-app-settings.png)

2. Under **Upload your code**, select **Upload** and provide:
   
   | Parameter            | Value |
   |----------------------|------------------------------------------------|
   | **Upload your code** | `Select` |
   | **Version label**    | `my-eb-app-source` |
   | **Public S3 URL**    | `Select` |
   | **S3 URL**           | `S3 object link` (from **wordpress-beanstalk.zip** upload) |

📷 [**Elastic Beanstalk S3 Settings Screenshot**](./images/eb-s3-settings.png)

3. Choose **Single Instance (free-tier eligible)** under **Presets**.

📷 [**Elastic Beanstalk Presets Screenshot**](./images/eb-presets.png)

4. Click **Next**.

---

## **🛠️ Step 3: Configure Service Access**
1. Select **Use new service role** (leave default).  
2. Select **ElasticBeanStalkInstanceRoleWeb** (previously created).  
3. Click **Next**.

📷 [**Elastic Beanstalk Service Role Selection Screenshot**](./images/eb-service-role.png)

---

## **🛠️ Step 4: Configure Networking**
1. Choose **TargetVPC** from the drop-down.
2. Select **Public IP address**.
3. Choose **TargetVPC-public-a** in **us-west-2a** Availability Zone.

📷 [**Elastic Beanstalk Networking Screenshot**](./images/eb-network.png)

4. Scroll down to **Database Settings** and select:
   - **TargetVPC-private-a-db**
   - **TargetVPC-private-b-db**

📷 [**Elastic Beanstalk Database Subnets Screenshot**](./images/eb-db-subnets.png)

5. Click **Next**.

---

## **🛠️ Step 5: Configure Scaling and Instance Settings**
1. Select **AMI ID**:  
ami-0c493115dacb8e9bd

- Modify AMI-ID if necessary to match your AWS Region.

2. Confirm **Single Instance** is selected.

📷 [**Elastic Beanstalk Auto Scaling Screenshot**](./images/eb-auto-scaling.png)

3. Click **Next**.

---

## **🛠️ Step 6: Configure Environment Variables**
1. Scroll to **Environment Properties**.
2. Add the following **database credentials**:

| Parameter       | Value |
|---------------|-----------------------------------------------|
| `RDS_DB_NAME`  | `wordpress-db` |
| `RDS_HOSTNAME` | **Your RDS Endpoint** *(from RDS console)* |
| `RDS_USERNAME` | `admin` |
| `RDS_PASSWORD` | **Your RDS Password** |
| `RDS_PORT`     | `3306` |

📷 [**Elastic Beanstalk Environment Variables Screenshot**](./images/eb-env-variables.png)

3. Click **Next**.

---

## **🛠️ Step 7: Review and Launch**
1. **Review configuration** to ensure everything is correct.
2. Click **Submit**.

📷 [**Elastic Beanstalk Review and Submit Screenshot**](./images/eb-review-submit.png)

---

## **🚀 Step 8: Update RDS Security Group**
To allow MySQL traffic from **Elastic Beanstalk**, update the **RDS Security Group**.

### **🔹 Modify Security Group**
1. Open **AWS Console** → **RDS** → **Databases**.
2. Click **Your RDS Database**.
3. Under **Connectivity & Security**, click **VPC Security Groups**.
4. Click **Security Group ID**.
5. Click **Edit Inbound Rules**.
6. Add the following rule:

| Type         | Protocol | Source |
|-------------|---------|------------------------------------|
| **MYSQL/Aurora** | **TCP** | **Elastic Beanstalk Security Group** |

📷 [**Elastic Beanstalk RDS Security Group Screenshot**](./images/eb-rds-security-group.png)

7. Click **Save Rules**.

---

## **✅ Next Steps**
🎉 **Congratulations!** I have successfully:
✅ Launched an **Elastic Beanstalk environment**.  
✅ Configured **Auto Scaling, Networking, and Environment Variables**.  
✅ Connected **Elastic Beanstalk to my RDS database**.  

➡️ **[Manage Elastic Beanstalk Environment](./replatform-eb-manage.md)**

