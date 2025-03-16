# **🚀 Replatform - AWS Elastic Beanstalk (EB)**

## **📌 Overview**
In this section, I will migrate my WordPress-based web application from an EC2 instance to **AWS Elastic Beanstalk**. Elastic Beanstalk is a fully managed service that simplifies **deployment**, **scaling**, and **management** of applications.

✅ **Automated Deployment & Scaling**  
✅ **Supports multiple platforms (PHP, Java, Node.js, etc.)**  
✅ **Retains full control over underlying AWS resources**  

📷 [**Beanstalk Overview](images/beanstalk-overview.png)

---

## **📌 Permissions Required**
Before proceeding, I must ensure my **IAM permissions** are set up correctly.

### **🔹 Service Role**
Elastic Beanstalk requires a **service role** to manage AWS resources on my behalf.

### **🔹 Instance Profile**
Each EC2 instance within Beanstalk must have an **instance profile** to:
- Retrieve application versions from S3
- Upload logs to S3
- Communicate with other AWS services

🔗 **[IAM Configuration Guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/iam-roles.html)**

---

## **🛠️ Step 1: Prepare the Source Code**
Before deploying the application, I need to **package** it properly for Beanstalk.

📌 **Steps to Prepare WordPress for Deployment**:
1️⃣ **Log into my current WordPress instance (EC2)**  
2️⃣ **Navigate to `/var/www/html` and zip the application files**  
```bash
cd /var/www/html
zip -r wordpress-app.zip .
```
3️⃣ ** Download the ZIP file locally for later upload to Beanstalk** 

## **🛠️ Step 2: Upload the Source Code Version**
📌 **Upload the ZIP file to Elastic Beanstalk.**

1️⃣ **In AWS Console, go to Services > Elastic Beanstalk** 
2️⃣ **Click Applications > Create Application** 
3️⃣ **Set Application Name: wordpress-app** 
4️⃣ **Click Create** 

📷 Create Beanstalk Application

5️⃣ **Under "Create a New Environment"** 

Environment Name: wordpress-env
Platform: PHP 7.4
Upload Code: Choose the wordpress-app.zip file
Click "Create Environment"
📷 Upload Application Version

🛠️ Step 3: Create an Instance Role
📌 Grant EC2 instances permission to interact with AWS services.

1️⃣ **Navigate to AWS IAM** 
2️⃣ **Click Roles > Create Role** 
3️⃣ **Choose AWS Service > EC2** 
4️⃣ **Attach Policies:** 

AWSElasticBeanstalkFullAccess
AmazonS3FullAccess
CloudWatchLogsFullAccess
5️⃣ **Role Name: aws-elasticbeanstalk-ec2-role** 
6️⃣ **Click Create Role** 
📷 Create IAM Role

🛠️ Step 4: Launch Beanstalk Environment
📌 Deploy my application using Elastic Beanstalk.

1️⃣ **In AWS Console, go to Elastic Beanstalk > Applications** 
2️⃣ **Select wordpress-app** 
3️⃣ **Click Environments > Create a new environment** 
4️⃣ **Choose "Web server environment"** 
5️⃣ **Select PHP 7.4 as the platform** 
6️⃣ **Attach the instance role (aws-elasticbeanstalk-ec2-role)** 
7️⃣ **Click Create Environment** 

📷 Launch Beanstalk Environment

🛠️ Step 5: Review and Manage the Environment
📌 Monitor and manage the running environment.

1️⃣ **Go to Elastic Beanstalk > Environments** 
2️⃣ **Select wordpress-env** 
3️⃣ **Click Monitoring to view metrics** 
4️⃣ **Check logs and health status** 

📷 Beanstalk Environment Monitoring

🛠️ Troubleshooting
🔹 Issue: Database Connection Errors
If my WordPress application fails to connect to the database: 
1️⃣ **Ensure the RDS database security group allows inbound connections from Beanstalk** 
2️⃣ **Check wp-config.php and update the database credentials** 
```bash
nano /var/www/html/wp-config.php
```
```php
define('DB_NAME', 'wordpress-db');
define('DB_USER', 'admin');
define('DB_PASSWORD', 'VeryHardPassword');
define('DB_HOST', 'my-rds-endpoint.amazonaws.com');
```
🔹 Issue: Load Balancer Not Routing Traffic
1️⃣ **Check Load Balancer Target Group under EC2 > Load Balancers** 
2️⃣ **Ensure the Beanstalk instance security group allows HTTP/HTTPS traffic** 
3️⃣ **Validate the Elastic Beanstalk logs for errors** 

📷 Beanstalk Logs for Troubleshooting

📌 Next Steps
➡️ **[Prepare Source Code for AWS Elastic Beanstalk Migration](../docs/replatform-eb-prepare.md)** 
