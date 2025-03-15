# **🚀 Prepare Source Code for AWS Elastic Beanstalk Migration**

## **📌 Overview**
Since AWS Elastic Beanstalk is a managed service, I don’t need to manually manage servers or infrastructure. Instead, I can **directly deploy** my application.  

In this step, I will:
✅ **Install necessary tools**  
✅ **Prepare my source code for deployment**  
✅ **Create a source code bundle**  

---

## **🛠️ Step 1: Install Necessary Toolset**
Before migrating my application to **AWS Elastic Beanstalk**, I need to install some required tools on the **Source Webserver** instance.

### **🔹 Connect to Source Webserver**
I will connect to my **Source Webserver** using either:
- **SSH** (For [Windows](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesWindows.html) | [Mac OS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html))  
- **AWS Session Manager** (recommended for browser-based access)
  
📌 **Steps to connect using AWS Session Manager**:
1. Open the **Amazon EC2 Console**: [🔗 AWS EC2 Console](https://console.aws.amazon.com/ec2/)
2. In the left panel, select **Instances**.
3. Select the **Source Webserver** instance and click **Connect**.
4. Choose **Session Manager** as the connection method.
5. Click **Connect**.

---

### **🔹 Install Required Packages**
Once connected, I will install:
1️⃣ **`zip`** – to package my source code  
2️⃣ **`awscli`** – to interact with AWS services like S3  

```bash
sudo apt update -y
sudo apt install -y zip awscli
```
📷 AWS CLI Installation Screenshot

🛠️ Step 2: Create a Development Environment
Instead of modifying my live production environment, I will create a separate development folder for migrating my application.
```bash
mkdir /tmp/myapp_beanstalk
cp -r /var/www/html/* /tmp/myapp_beanstalk/
```
📌 This will simulate a separate environment for testing before full deployment.

🛠️ Step 3: Update Application Configuration
Now, I will update WordPress database settings to use AWS Elastic Beanstalk environment variables instead of hardcoded values.

🔹 Modify wp-config.php
```bash
cd /tmp/myapp_beanstalk
sudo nano wp-config.php
```
🔹 Replace Existing Database Configuration
📌 The existing database settings might look like this:
```php
define('DB_NAME', 'wordpress-db');
define('DB_USER', 'wordpress-user');
define('DB_PASSWORD', 'AWSRocksSince2006');
define('DB_HOST', '10.0.0.68');
```
🚨 Problem:
This hardcodes database credentials, making it less secure and harder to change.

✅ Best Practice: Use Environment Variables
📌 I will replace the above code with:
```php
define('DB_NAME', $_SERVER['RDS_DB_NAME']);
define('DB_USER', $_SERVER['RDS_USERNAME']);
define('DB_PASSWORD', $_SERVER['RDS_PASSWORD']);
define('DB_HOST', $_SERVER['RDS_HOSTNAME'] . ':' . $_SERVER['RDS_PORT']);
```
📌 Why?
✅ No hardcoded credentials
✅ Application changes do not require code modification
✅ Easier database connection management

I will then save and exit (CTRL + X, then Y and Enter).

🛠️ Step 4: Create a Source Code Bundle
AWS Elastic Beanstalk requires a zip package of my application code for deployment.

🔹 Create ZIP Archive
```bash
cd /tmp/myapp_beanstalk
zip -r ../wordpress-beanstalk.zip * .[^.]*
```
📌 Confirm ZIP File Creation:
```bash
cd /tmp/
ls -ltr
```
📷 ZIP File Validation Screenshot

✅ Next Steps
➡️ Upload Source Code to S3




