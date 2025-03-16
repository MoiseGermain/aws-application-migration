# 🚀 Deploy AWS Application Discovery Service (ADS)

In this section, I will install the **AWS Discovery Agent** on my web and database servers to start collecting system configuration and performance data. This will allow me to analyze my on-premises environment before migration.

---

## **1️⃣ Install the Discovery Agent on Web Server**  

### **🔹 Connect to the Web Server**  
1️⃣ Navigate to the **EC2 Console**.  
2️⃣ Select the **Source-Webserver** instance and click **Connect** (top-right corner).  
3️⃣ Choose the **Session Manager** tab and click **Connect**.  

📌 *Now, I'm inside the instance shell session.*

---

### **🔹 Switch to Ubuntu User**
```bash
sudo su - ubuntu
```
🔹 Download and Extract the AWS Discovery Agent
```bash 
curl -o ./aws-discovery-agent.tar.gz https://s3-us-west-2.amazonaws.com/aws-discovery-agent.us-west-2/linux/latest/aws-discovery-agent.tar.gz
tar -xzf aws-discovery-agent.tar.gz 
```
📌 This fetches the latest AWS Discovery Agent and extracts it for installation.

🔹 Install the Agent and Authenticate with AWS IAM
Before running the command below, I will replace <AWS_key_ID> and <AWS_secret_key> with the credentials obtained from the IAM Console.
```bash
sudo bash install -r us-west-2 -k <AWS_key_ID> -s <AWS_secret_key>
```
📌 If I see an error stating "dpkg frontend is locked by another service", I will wait a few minutes and retry.

🔹 Verify That the Agent Is Running
```bash
sudo systemctl status aws-discovery-daemon.service
```
✅ I should see that the agent process is active (running).

## **2️⃣ Verify Discovery in AWS Application Discovery Service**

1️⃣ Open AWS Console and navigate to:
➝ Migration Hub → Discover → Data Collectors

2️⃣ If prompted to select a Migration Hub home Region, I will choose US West (Oregon).

3️⃣ In the Data Collectors section, I will select the Discovery Agents tab.

4️⃣ I will verify that:
✅ Collection status is Collecting
✅ Health status is Running

📌 Now, the agent is actively collecting and syncing data from my Web Server.

## **3️⃣ Install the Discovery Agent on the Database Server**
📌 I will now repeat the process for the Source-DBServer instance.

🔹 Connect to the Database Server
1️⃣ Navigate to the EC2 Console.

2️⃣ Select the Source-DBServer instance and click Connect.

3️⃣ Choose the Session Manager tab and click Connect.

📌 Now, I'm inside the instance shell session.

🔹 Switch to Ubuntu User
```bash
sudo su - ubuntu
```
🔹 Download and Extract the AWS Discovery Agent
```bash
curl -o ./aws-discovery-agent.tar.gz https://s3-us-west-2.amazonaws.com/aws-discovery-agent.us-west-2/linux/latest/aws-discovery-agent.tar.gz
tar -xzf aws-discovery-agent.tar.gz
```
📌 This fetches the latest AWS Discovery Agent and extracts it for installation.

🔹 Install the Agent and Authenticate with AWS IAM
Before running the command below, I will replace <AWS_key_ID> and <AWS_secret_key> with the credentials obtained from the IAM Console.
```bash
sudo bash install -r us-west-2 -k <AWS_key_ID> -s <AWS_secret_key>
```
📌 If I see an error stating "dpkg frontend is locked by another service", I will wait a few minutes and retry.

🔹 Verify That the Agent Is Running
```bash
sudo systemctl status aws-discovery-daemon.service
```
✅ I should see that the agent process is active (running).

## **4️⃣ Verify Discovery in AWS Application Discovery Service**
1️⃣ Open AWS Console and navigate to:
➝ Migration Hub → Discover → Data Collectors

2️⃣ If prompted to select a Migration Hub home Region, I will choose US West (Oregon).

3️⃣ In the Data Collectors section, I will select the Discovery Agents tab.

4️⃣ I will verify that:
✅ Collection status is Collecting
✅ Health status is Running

📌 Now, the agent is actively collecting and syncing data from my Database Server.

✅ Next Steps
➡️ Proceed to **[Review Collected Data](../docs/review-collected-data.md)**




