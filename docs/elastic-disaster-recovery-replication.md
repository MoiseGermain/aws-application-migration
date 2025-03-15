# **🔹 Installing AWS Replication Agents**

## **📌 Overview**
To enable AWS **Elastic Disaster Recovery (EDR)**, I must install the **AWS Replication Agent** on each source server. This will allow real-time replication of data to the **Disaster Recovery (DR) Region** (`us-west-1`).

📌 **Ensure that the AWS Region is set to `us-west-2 (Oregon)` before proceeding.**  
📷 **[Switch AWS Region](./images/switch-region.png)**  

---

## **📍 Step 1: Install Replication Agent on Source Web Server**
1️⃣ **Change AWS Region to `us-west-2` (Oregon)** to access the source EC2 servers.  
2️⃣ In **AWS Console**, navigate to:  
   **Services → EC2 → Instances**  
3️⃣ Select **Source-Webserver**, then click **Connect**.  
📷 **[Select Web Server](./images/select-webserver.png)**  
4️⃣ In the **Session Manager** tab, click **Connect**.  

📷 **[Connect to Web Server](./images/select-webserver.png)**  

5️⃣ Copy and execute the following commands in the terminal:

```bash
sudo su -
wget -O ./aws-replication-installer-init https://aws-elastic-disaster-recovery-us-west-1.s3.us-west-1.amazonaws.com/latest/linux/aws-replication-installer-init
chmod +x aws-replication-installer-init; sudo ./aws-replication-installer-init
```
6️⃣ At the AWS Region Name prompt, enter:
➝ us-west-1
7️⃣ At the To replicate all disks prompt, press Enter.

📌 The installation will take a few minutes to complete.
📷 Installing Replication Agent

📍 Step 2: Verify Web Server Replication
1️⃣ Change AWS Region to us-west-1 (N. California).
📷 Switch AWS Region

2️⃣ In AWS Console, navigate to:
Services → AWS Elastic Disaster Recovery
3️⃣ Click Source Servers in the left panel.
4️⃣ Verify that the Web Server appears in the list.
📷 Web Server in Replication

🔹 Understanding Server Status
Status	Description
Ready	Server is fully replicated and ready for recovery.
Ready-lag	Server is ready but experiencing a slight delay.
Init-sync	Initial synchronization is in progress.
Disconnect	Server is not connected to AWS EDR.
Not-ready	Major error preventing replication.
📌 Wait until the Web Server transitions from Init-sync to Ready. This may take 20-30 minutes.
📷 Web Server Ready

📍 Step 3: Install Replication Agent on Source Database Server
1️⃣ Change AWS Region to us-west-2 (Oregon).
📷 Switch AWS Region

2️⃣ In AWS Console, navigate to:
Services → EC2 → Instances
3️⃣ Select Source-DBServer, then click Connect.
📷 Select Database Server
4️⃣ In the Session Manager tab, click Connect.

📷 Connect to Database Server

5️⃣ Copy and execute the following commands in the terminal:
```
sudo su -
wget -O ./aws-replication-installer-init https://aws-elastic-disaster-recovery-us-west-1.s3.us-west-1.amazonaws.com/latest/linux/aws-replication-installer-init
chmod +x aws-replication-installer-init; sudo ./aws-replication-installer-init
```
6️⃣ At the AWS Region Name prompt, enter:
➝ us-west-1
7️⃣ At the To replicate all disks prompt, press Enter.

📌 The installation will take a few minutes to complete.
📷 Installing Replication Agent

📍 Step 4: Verify Database Server Replication
1️⃣ Change AWS Region to us-west-1 (N. California).
📷 Switch AWS Region

2️⃣ In AWS Console, navigate to:
Services → AWS Elastic Disaster Recovery
3️⃣ Click Source Servers in the left panel.
4️⃣ Verify that the Database Server appears in the list.
📷 Database Server in Replication

📌 Wait until the Database Server transitions from Init-sync to Ready. This may take 20-30 minutes.
📷 Database Server Ready

🚀 Next Steps
Now that both servers are fully replicated, I will proceed with:
➡️ Configuring EC2 launch settings for the Disaster Recovery environment.

📌 Proceed to Next Step: Configuring EC2 Launch Settings
