# **🔹 Initiating a Disaster Recovery Job**

## **📌 Overview**
In the event of a disaster, I will need to **fail over to AWS** using **AWS Elastic Disaster Recovery (AWS DRS)**. This process ensures that my recovery systems are ready when needed. 

AWS DRS allows me to:
- Launch recovery instances using the latest data or **point-in-time snapshots**.
- Recover **one or multiple servers** simultaneously.
- Delete and relaunch **previous recovery instances** to reflect the latest data.

**⚠️ Important:** Data replication continues after recovery, ensuring new changes are stored in the **staging area subnet** and not directly on the launched recovery instances.

---

## **📍 Step 1: Launch Recovery Web Server Instance**
1️⃣ In the **AWS Console**, navigate to:  
   ➝ **Services → AWS Elastic Disaster Recovery**  
2️⃣ Click **Source Servers** in the left navigation panel.  
3️⃣ Select the **Web Server hostname**.  
4️⃣ Click **Initiate Recovery Job**, then select **Initiate Recovery**.  
📷 **[Initiate Web Server Recovery](./images/select-ws-job.png)**  

5️⃣ In the **Points in Time** section, choose:  
   ✅ **Use Most Recent Data**  
6️⃣ Click **Initiate Recovery**.  
📷 **[Select Recovery Data Point](./images/point-in-time.png)**  

7️⃣ Return to **Source Servers**, click **View Job Details** to track progress.  
📷 **[View Job Status](./images/ws-job-details.png)**  

💡 **The recovery job will take approximately `10 minutes` to complete.**

---

## **📍 Step 2: Launch Recovery Database Server Instance**
1️⃣ In **AWS Console**, navigate to:  
   ➝ **Services → AWS Elastic Disaster Recovery**  
2️⃣ Click **Source Servers** in the left navigation panel.  
3️⃣ Select the **Database Server hostname**.  
📷 **[Select Database Server](./images/db-recovery.png)**  

4️⃣ Click **Initiate Recovery Job**, then select **Initiate Recovery**.  
📷 **[Initiate Database Server Recovery](./images/select-db-job.png)**  

5️⃣ In the **Points in Time** section, choose:  
   ✅ **Use Most Recent Data**  
6️⃣ Click **Initiate Recovery**.  
📷 **[Select Recovery Data Point](./images/point-in-time-db.png)**  

7️⃣ Return to **Source Servers**, click **View Job Details** to track progress.  
📷 **[View Job Status](./images/db-job-details.png)**  

💡 **The recovery job will take approximately `10 minutes` to complete.**

---

## **✅ Verifying the Recovery**
After launching both **Web Server** and **Database Server** recovery instances:
- Check the **Source Servers** page for the **Ready** status.
- Verify that both servers have been successfully recovered.  
📷 **[Recovery Result](./images/recover-result.png)**  

---

## **🚀 Next Steps**
Now that the recovery instances have launched, I will proceed with:  
➡️ **Configuring the Application on the Recovery Web Server**  

📌 **[Proceed to Next Step: Configuring Recovered Instances](./elastic-disaster-recovery-configure.md)**  
