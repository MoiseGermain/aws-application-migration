# 🛠 **Configure Source Database for AWS DMS**

## **Overview**
To ensure **minimal downtime** for database migration, I'll use **continuous replication of changes** (Change Data Capture - CDC) from the **source database** to the **target database**.

🔗 **[What is Change Data Capture (CDC)?](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Source.MySQL.html#CHAP_Source.MySQL.CDC)**

---

## **🔹 Step 1: Connect to Source Database Server**
### **1️⃣ Navigate to EC2 Console**
1. Open **AWS Console** → **Services** → **Compute** → **EC2**.
2. Select **Instances** from the left menu.
3. Find the instance named **Source-DBServer**.
4. Click **Connect**.
5. Select the **Session Manager** tab.
6. Click **Connect**.

🔗 **[AWS EC2 Connect](assets/aws-ec2-connect.png)**

📌 If using **SSH**, modify **DB-SG Security Group** to allow connection from my **public IP**.

---

## **🔹 Step 2: Enable CDC on MySQL Source Database**
In the **EC2 terminal**, I will **grant privileges** to the `wordpress-user` database user for **CDC functionality**.

### **1️⃣ Connect to MySQL**
```bash
sudo mysql -u root -pAWSRocksSince2006
```
2️⃣ Grant Replication Privileges
```sql

GRANT REPLICATION CLIENT ON *.* TO 'wordpress-user';
GRANT REPLICATION SLAVE ON *.* TO 'wordpress-user';
GRANT SUPER ON *.* TO 'wordpress-user';
EXIT;
```
🔹 Step 3: Enable Binary Logging for MySQL
1️⃣ Create Binary Log Directory
```bash

sudo su - 
mkdir /var/lib/mysql/binlogs
chown -R mysql:mysql /var/lib/mysql/binlogs
exit
```
📌 MySQL binary logs track database changes, crucial for continuous replication.

2️⃣ Modify MySQL Configuration for Binary Logs
```bash
sudo su -
cp /etc/mysql/mysql.conf.d/mysqld.cnf /etc/mysql/my.cnf
chown -R mysql:mysql /etc/mysql/my.cnf
cat <<EOF >> /etc/mysql/my.cnf
server_id=1
log-bin=/var/lib/mysql/binlogs/log
binlog_format=ROW
expire_logs_days=1
binlog_checksum=NONE
binlog_row_image=FULL
log_slave_updates=TRUE
performance_schema=ON
EOF
```

3️⃣ Restart MySQL Service
```bash
sudo systemctl restart mysql
📌 This will cause a few seconds of downtime for the source database.
```
🔹 Step 4: Verify Configuration Changes
1️⃣ Check Binary Logging Status
```bash
sudo mysql -u root -pAWSRocksSince2006
```
2️⃣ Run Verification Queries
```sql
SELECT variable_value AS "BINARY LOGGING STATUS (log-bin) :: "
FROM performance_schema.global_variables WHERE variable_name='log_bin';

SELECT variable_value AS "BINARY LOG FORMAT (binlog_format) :: "
FROM performance_schema.global_variables WHERE variable_name='binlog_format';

EXIT;
```
🔗 Binary Logging Status Check

🎯 Next Steps
➡️ **[Create Source and Target Endpoints](./create-dms-endpoints.md )**
