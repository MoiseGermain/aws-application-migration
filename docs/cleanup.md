# **🔹 Cleanup Guide**

At the end of your migration project, it’s important to **delete all resources** that were created. Follow the steps below to clean up resources from different AWS services.

---

## **📌 AWS Application Migration Service (MGN)**
1. Navigate to **AWS MGN Console**.
2. Select the server(s).
3. Click **Actions → Mark as archived** and confirm.

---

## **📌 AWS RDS**
1. Navigate to **AWS RDS Console**.
2. **Uncheck** the **Deletion Protection** checkbox (apply changes immediately).
3. Delete created databases:
   - **Do not** take a final snapshot.
   - **Do not** retain automated backups.

---

## **📌 AWS Database Migration Service (DMS)**
1. **Stop** and delete created **replication tasks** (wait until tasks are deleted).
2. Delete **replication instances** (wait until they are deleted).
3. Delete created **endpoints**.
4. Delete **subnet groups**.
5. Go to **AWS DMS Dashboard** to confirm that everything was deleted.

---

## **📌 Amazon Elastic File System (EFS)**
1. Navigate to **Amazon EFS Console**.
2. Delete the **Elastic File System** you created.

---

## **📌 AWS Elastic Container Service (ECS)**
1. Delete created **services**.
2. Delete **task definitions**.
3. Delete **clusters**.

---

## **📌 AWS EC2**
1. Terminate all created **EC2 instances** (including those with `"CloudEndure"` prefix).
2. Delete created **Load Balancers**.

---

## **📌 AWS CloudFormation**
1. Delete the **ApplicationMigrationWorkshop** stack.

---

## **📌 AWS Elastic Beanstalk**
1. Delete the **Elastic Beanstalk application**.
2. Delete the **S3 bucket** that stored the **source code**.

---

## **📌 AWS Migration Hub (Application Discovery Service Cleanup)**
To clean up resources from AWS **Application Discovery Service**, follow these steps:

### **🛠 Run Cleanup Script in AWS CloudShell**
1. **Launch AWS CloudShell**.
2. **Download & Run** the cleanup script:

   ```bash
   wget https://ws-assets-prod-iad-r-pdx-f3b3f9f1a7d6a3d0.s3.us-west-2.amazonaws.com/c6bdf8dc-d2b2-4dbd-b673-90836e954745/scripts/cleanupads.py
   python cleanupads.py
``
❗ Troubleshooting
If you get an error:
"Requested agent is either actively reporting health or collecting data"
Solution: Wait at least 1 hour before retrying or force cleanup using -f:
```
python cleanupads.py -f
```
If servers reappear, they may still be actively reporting to ADS.
Solution: Check the Data collectors dashboard under AWS Migration Hub and ensure no active agents are reporting.

📌 AWS Migration Hub (Final Cleanup)
Navigate to AWS Migration Hub → Discover → Applications.
Select the application.
Click Actions → Remove application.
📌 Final Review
After completing all cleanup steps:

Review your AWS account to ensure no remaining resources exist.
Provide anonymous feedback to improve this workshop.
✅ All resources should now be cleaned up! 🚀
