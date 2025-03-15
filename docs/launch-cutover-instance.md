# **🚀 Launch Cutover Instance in AWS MGN**

## **📌 Overview**
Now that I have successfully **validated the test instance**, it's time to execute the **final migration**.  
This involves launching a **cutover instance**, which is the final EC2 instance after the **rehost migration** in **AWS Application Migration Service (MGN)**.

---

## **1️⃣ Launch the Cutover Instance**
📌 **To launch the cutover instance:**
1. Navigate to **AWS Console** → **Migration & Transfer** → **Application Migration Service**.
2. Under **Source servers**, my server should be in **"Ready for cutover" state**.
3. Click on the **hostname** of my source server.
4. Click on **Test and Cutover** → Select **Launch cutover instance**.
5. Confirm the pop-up window.

✅ **The cutover instance is now launching!**  

---

## **2️⃣ Monitor the Cutover Job**
📌 **To track the cutover launch:**
1. Under **Lifecycle**, click the **Job ID** in the **Cutover** section.
2. In the **Job details screen**, I can review:
   - **Start and completed time**
   - **Events log**
   - **Additional details for each event**

⏳ **The MGN cutover launch will take around ~15 minutes to complete.**  

---

## **3️⃣ Check the Launch History**
📌 **To view the migration history:**
1. Navigate to **AWS Console** → **Migration & Transfer** → **Application Migration Service**.
2. Click on **Launch history** in the left menu.
3. Review all **previous migration jobs** and confirm they are marked as **completed**.

✅ **All migration tasks should now be completed!**  

---

## **4️⃣ Verify the Migrated EC2 Instance**
📌 **To check the final migrated server:**
1. Navigate back to **AWS Console** → **Application Migration Service**.
2. Under **Source servers**, my **Launch status** should now be **"Launched"**.
3. Click **View in EC2 Console** to see the rehosted instance.

✅ **The cutover instance is now running in my target AWS environment!**  

---

## **5️⃣ (Optional) Revert to "Ready for Cutover"**
📌 **If there are any issues with the launch, I can revert the migration:**
1. Navigate to **AWS Console** → **Application Migration Service**.
2. Click on **Test and Cutover** → Select **Revert to "Ready for cutover"**.
3. Confirm the pop-up.

🔹 **This is useful if I need to troubleshoot the cutover instance and restart the migration process.**

---

## **🎯 Next Steps**
Now that my **migrated server is running in AWS**, it's time to **reconfigure it for full functionality**.

➡️ **[Configure Migrated Server](./configure-migrated-server.md) 🔧**
