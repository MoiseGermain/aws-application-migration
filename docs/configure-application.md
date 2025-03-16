# **🔧 Configure Migrated Application**

## **📌 Overview**
After launching the cutover instance, **AWS Application Migration Service (MGN)** has created the final EC2 instance in my **target environment**.  
However, my workload is still configured to the **source environment**.  

Now, I need to update my **application configuration** to connect to the **migrated database** running on **Amazon RDS**.

---

## **1️⃣ Connect to the Webserver**
📌 **To access the migrated webserver:**
1. Navigate to **AWS Console** → **EC2** → **Instances**.
2. Select the **Webserver** instance and click **Connect**.
3. Choose the **Session Manager** tab and click **Connect** to open a terminal session.

✅ **I am now inside my migrated webserver instance.**

---

## **2️⃣ Update the WordPress Configuration**
📌 **To configure the application to use the migrated database:**
1. Switch to the root user:
   ```bash
   sudo su -

2.Update the WordPress database credentials in wp-config.php:
```bash
sed -i "s|^.*DB_USER.*$|define( 'DB_USER', '<USERNAME>' );|" /var/www/html/wp-config.php
sed -i "s|^.*DB_PASSWORD.*$|define( 'DB_PASSWORD', '<PASSWORD>' );|" /var/www/html/wp-config.php
sed -i "s|^.*DB_HOST.*$|define( 'DB_HOST', '<RDS_ENDPOINT>' );|" /var/www/html/wp-config.php
echo "define('WP_SITEURL', 'http://$(curl -s http://169.254.169.254/latest/meta-data/public-hostname)');" >> /var/www/html/wp-config.php
echo "define('WP_HOME', 'http://$(curl -s http://169.254.169.254/latest/meta-data/public-hostname)');" >> /var/www/html/wp-config.php
```
📌 Replace the placeholders (<USERNAME>, <PASSWORD>, <RDS_ENDPOINT>) with the correct values from the AWS RDS console.

✅ The application is now configured to use the migrated database.
3️⃣ Update Security Group Rules for Database Access
📌 To allow the webserver to connect to the RDS database:

Navigate to AWS Console → EC2 → Security Groups.
Select DB-SG (the security group for the RDS instance).
Click Edit inbound rules.
Add a new inbound rule with the following values:
Type: MYSQL/Aurora
Protocol: TCP
Port Range: 3306
Source: Select the MigratedWebserver-SG security group.
✅ The webserver can now communicate with the database.

4️⃣ Verify the Migrated Application
📌 To confirm the webserver is running:

1.Navigate to AWS Console → EC2 → Instances.
2.Select the Webserver instance.
3.Go to the Networking tab and copy the Public IPv4 DNS.
4.Open a web browser and go to:
```cpp
http://<Public-IPv4-DNS>
```
🚨 Important:

The EC2 console provides the public DNS with https://, but my application is not configured for HTTPS.
I must access the application using http:// instead.
✅ If the application loads without errors, the migration was successful!

5️⃣ Troubleshooting Steps
If I encounter any errors, I will check the following:

Database Connection Issues

Ensure the RDS database credentials (DB_USER, DB_PASSWORD, DB_HOST) in /var/www/html/wp-config.php are correct.
Verify the RDS database security group is set to DB-SG.
Security Group Issues

Ensure DB-SG allows inbound MySQL connections (TCP/3306) from MigratedWebserver-SG.
Networking Issues

Confirm that the Webserver EC2 instance is deployed in TargetVPC-public-subnet-a.
Check RDS Endpoint

Go to AWS Console → RDS → Databases.
Select database-1 and check the Endpoint and Port.
✅ Once my application is functional, I can finalize the migration process!

🎯 Next Steps
Now that my application is fully functional, it's time to finalize the cutover process in AWS Application Migration Service (MGN).

➡️ **[Finalize Cutover 🎉](./finalize-cutover.md**
