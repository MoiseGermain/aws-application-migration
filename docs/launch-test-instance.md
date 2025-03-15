# **🚀 Launch Test Instance in AWS MGN**

## **📌 Overview**
Now that everything is ready, I will **rehost my source application server** to the target AWS environment using **AWS Application Migration Service (MGN)**.  
This process involves launching a **test instance** to validate that MGN successfully migrated my application.

## **1️⃣ AWS MGN Lifecycle States**
Each source server in **AWS MGN** follows a specific **migration lifecycle**:

| **State**                 | **Description** |
|---------------------------|----------------|
| **Not Ready**             | Initial Sync is in progress. Replication has not started yet. |
| **Ready for Testing**     | Data replication has started. Test or cutover instances can now be launched. |
| **Test in Progress**      | A test instance is currently being launched. |
| **Ready for Cutover**     | Test is complete. A cutover instance can now be launched. |
| **Cutover in Progress**   | A cutover instance is currently being launched. |
| **Cutover Complete**      | The cutover instance has been successfully migrated. |

🔹 **More details about each state:** [AWS MGN Lifecycle States Documentation](https://docs.aws.amazon.com/mgn/latest/ug/mgn-server-lifecycle.html)

---

## **2️⃣ Launch the Test Instance**
📌 **To launch a test instance:**
1. Navigate to **AWS Console** → **Migration & Transfer** → **Application Migration Service**.
2. Under **Source servers**, my **server should be in "Ready for testing" state**.
3. Click on the **hostname** of my source server.
4. Click on **Test and Cutover** → Select **Launch test instance**.
5. Confirm the pop-up window.

✅ **The test instance is now launching!**  

---

## **3️⃣ Monitor Test Launch Progress**
📌 **To track the test launch:**
1. Under **Lifecycle**, click the **Job ID**.
2. In the **Job details screen**, I can review:
   - **Start and completed time**
   - **Events log**
   - **Additional details for each event**

⏳ **The MGN test launch will take around ~15 minutes to complete.**  

---

## **4️⃣ (Optional) Verify Test Instance in EC2**
📌 **To check the test instance in AWS EC2:**
1. Navigate to **AWS Console** → **Compute** → **EC2**.
2. Under **Instances**, select the one named **Webserver**.
3. Verify that:
   - **The instance is running.**
   - **The public IP is assigned correctly.**
   - **The instance is in the correct VPC and subnet.**
4. (Optional) **Connect to the instance** and verify that all files are intact.

---

## **5️⃣ Validate the Web Application**
📌 **To test the web server in a browser:**
1. Copy the **public IP address** of the test instance.
2. Paste it into my browser and hit enter.
3. If I see an **"Error establishing a database connection"**, it's expected because:
   - The application is not yet reconfigured to use the new database.

✅ **This confirms that AWS MGN successfully rehosted the source server!**  

---

## **6️⃣ Mark Test as Completed**
📌 **To finalize the test:**
1. Navigate back to **AWS Console** → **Application Migration Service**.
2. My source server should now be in **Testing in progress** state.
3. Click on **Test and Cutover** → Select **Mark as "Ready for cutover"**.
4. Confirm the pop-up.

⏳ **Wait ~5 minutes** for test instances to terminate.

✅ **The migration test is complete!**  
🎯 **Next step:** [Launch Cutover Instance](./launch-cutover-instance.md) 🚀
