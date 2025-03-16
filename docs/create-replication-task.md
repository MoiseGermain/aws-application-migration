# 🔄 **Create and Run a Replication Task in AWS DMS**

## **📌 Overview**
A **replication task** is required to move data from the **source database** to the **target database** in **AWS Database Migration Service (DMS)**. This is the **final step** before fully migrating our database.

In this section, I will:
✔️ **Configure the replication task**
✔️ **Set up table mappings**
✔️ **Enable continuous Change Data Capture (CDC)**
✔️ **Monitor replication progress**

---

## **🔹 Step 1: Create a Database Migration Task**
### **1️⃣ Navigate to AWS DMS**
1. **Open AWS Console** → **Services** → **Migration & Transfer** → **Database Migration Service**.
2. Select **Database migration tasks** from the left-hand menu.
3. Click **Create task**.

🔗 **[AWS DMS Migration Task Console](assets/dms-migration-task.png)**

---

## **🔹 Step 2: Configure Replication Task**
| **Parameter**              | **Value** |
|---------------------------|-----------|
| **Task Identifier**        | `replication-cdc` |
| **Replication Instance**   | `replication-instance` |
| **Source Endpoint**        | `source-endpoint` |
| **Target Endpoint**        | `target-endpoint` |
| **Migration Type**         | `Migrate existing data and replicate ongoing changes` |

📌 This configuration ensures **both initial migration and ongoing replication**.

🔗 **[DMS Task Settings](assets/dms-task-settings.png)**

---

## **🔹 Step 3: Configure Task Settings**
| **Parameter**                        | **Value** |
|--------------------------------------|-----------|
| **Target Table Preparation Mode**   | `Do nothing` |
| **Validation**                      | `Turn on` |
| **Task Logs**                        | `Turn on` |

📌 Enabling **Validation and Task Logs** ensures data integrity during migration.

---

## **🔹 Step 4: Configure Table Mappings**
1. **Select "Wizard mode"**.
2. Click **"Add new selection rule"**.
3. Select **"wordpress-db"** in the Schema dropdown.
4. If `wordpress-db` is not available, select **Enter schema** and manually type `wordpress-db`.

🔗 **[DMS Table Mapping](assets/dms-task-settings.png)**

---

## **🔹 Step 5: Disable Pre-Migration Assessment**
1. Scroll to **Premigration Assessment**.
2. **Disable** `Turn on premigration assessment`.

📌 This avoids unnecessary delays in the migration.

---

## **🔹 Step 6: Start the Migration Task**
1. Scroll to **Migration task startup configuration**.
2. Select **"Automatically on create"**.
3. Click **Create Task**.

📌 The replication task will start **automatically** after creation.

🔗 **[DMS Auto-Start Task](assets/dms-task-monitor.png)**

---

## **🔹 Step 7: Monitor Migration Progress**
1. Wait for the **Status** to change to:
   - ✅ **Load complete, replication ongoing**
   - ✅ **Progress: 100%**
2. Click on the **task details** to view:
   - Number of **replicated rows**
   - **Tables successfully migrated**

📌 This task **continuously replicates** changes to keep the **target database in sync**.

---

## **🎯 Next Steps**
✅ **The data is now migrated!** 🎉  
➡️ **[Migration Summary](./migration-summary.md)** 🚀
