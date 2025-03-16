# **🔹 Configuring EC2 Launch Settings for Disaster Recovery**

## **📌 Overview**
Now that the source servers have been added to **AWS Elastic Disaster Recovery (EDR)**, I need to configure the **EC2 launch settings**. These settings define how recovery instances will be launched when a disaster occurs.

📌 **Ensure that the AWS Region is set to `us-west-1 (N. California)` before proceeding.**  
📷 **[Switch AWS Region](./images/changed-region2.png)**  

---

## **📍 Step 1: Configure Launch Settings for Web Server**
1️⃣ In **AWS Console**, navigate to:  
   ➝ **Services → AWS Elastic Disaster Recovery**  
2️⃣ Click **Source Servers** in the left navigation panel.  
3️⃣ Select the **Web Server hostname**.  
📷 **[Select Web Server](./images/select-dr-ws.png)**  

4️⃣ Click the **Launch settings** tab.  
5️⃣ In the **EC2 Launch Template** section, click **Edit**.  
📷 **[Edit Web Server Launch Settings](./images/edit-ws-launch-settings.png)**  

### **🔹 Update Web Server Launch Settings**
| **Parameter**         | **Value** |
|----------------------|----------|
| **Subnet**           | `Elastic-DR-subnet-public2-us-west-1c` |
| **Security Groups**  | `DR-WebserverSG` |
| **Instance Type**    | `t3.small` |

📌 Expand the **Advanced settings** section and configure:  
| **Parameter**                | **Value** |
|-----------------------------|----------|
| **IAM Instance Profile**     | `migration-workshop-source-template-EC2InstanceProfile-xxx` |
| **Auto-assign Public IP**    | `Yes` |

📷 **[Updated Web Server Launch Settings](./images/ws-launch-settings.png)**  

6️⃣ Click **Update template** to save the changes.

---

## **📍 Step 2: Configure Launch Settings for Database Server**
1️⃣ In **AWS Console**, navigate to:  
   ➝ **Services → AWS Elastic Disaster Recovery**  
2️⃣ Click **Source Servers** in the left navigation panel.  
3️⃣ Select the **Database Server hostname**.  
📷 **[Select Database Server](./images/select-dr-db.png)**  

4️⃣ Click the **Launch settings** tab.  
5️⃣ In the **EC2 Launch Template** section, click **Edit**.  
📷 **[Edit Database Server Launch Settings](./images/edit-db-launch-settings.png)**  

### **🔹 Update Database Server Launch Settings**
| **Parameter**         | **Value** |
|----------------------|----------|
| **Subnet**           | `Elastic-DR-subnet-private2-us-west-1c` |
| **Security Groups**  | `DR-DBserverSG` |
| **Instance Type**    | `t3.micro` |

📌 Expand the **Advanced settings** section and configure:  
| **Parameter**                | **Value** |
|-----------------------------|----------|
| **IAM Instance Profile**     | `migration-workshop-source-template-EC2InstanceProfile-xxx` |

📷 **[Updated Database Server Launch Settings](./images/ws-launch-settings.png)**  

6️⃣ Click **Update template** to save the changes.

---

## **🚀 Next Steps**
The launch settings have been configured for both the **Web Server** and **Database Server**. Now, I will proceed with:  
➡️ **Initiating a Disaster Recovery Job**  

📌 **[Proceed to Next Step: Initiating a Disaster Recovery Job](./elastic-disaster-recovery-recovery.md)**  
