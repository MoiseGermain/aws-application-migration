# **🔄 Updating Server Details in AWS MGN**

## **📌 Overview**
After installing the **AWS Application Migration Service (MGN) Agent**, my source server is now registered with AWS MGN.  
This allows me to **monitor replication progress**, review server details, and **customize** how replication will be executed.

---

## **1️⃣ Explore Source Server Details**
📌 **To review the details of my source server:**
1. Navigate to **AWS Console** → **Migration & Transfer** → **Application Migration Service**.
2. Under **Source servers**, click on the hostname of my source server.

Now, I can explore different **tabs** for detailed insights:

- **Migration Dashboard:** Monitor replication progress.  
- **Server Info:** Review hardware profile, OS, and recommended EC2 instance type.  
- **Tags:** Manage AWS tags for my source server.  
- **Disk Settings:** View replicated disks and Amazon EBS volume type.  
- **Replication Settings:** Customize replication configurations.  

---

## **2️⃣ (Optional) Enable Post-Launch Actions**
📌 **Post-launch actions** allow AWS to execute scripts after launching a test or cutover instance.  
For this setup, I will enable **AWS CloudWatch Agent** to collect memory and swap utilization metrics.

### **🔹 Step 1: Create CloudWatch Agent Configuration**
1. Navigate to **AWS Console** → **Systems Manager** → **Parameter Store**.
2. Click **Create parameter**.
3. Enter **`cloudwatch-config`** as the parameter name.
4. Copy and paste the following JSON configuration into the **Value** field:
```json
{
    "agent": {
        "metrics_collection_interval": 10,
        "run_as_user": "cwagent"
    },
    "metrics": {
        "aggregation_dimensions": [["InstanceId"]],
        "metrics_collected": {
            "mem": {
                "measurement": ["mem_used_percent"],
                "metrics_collection_interval": 10
            },
            "swap": {
                "measurement": ["swap_used_percent"],
                "metrics_collection_interval": 10
            }
        }
    }
}
```
5.Click Create parameter.
🔹 Step 2: Enable Post-Launch Action
Navigate to AWS Console → Application Migration Service.
Select my source server → Click Post-launch settings tab → Click Edit.
Enable Install the Systems Manager agent and allow executing actions on launched servers.
Click Save settings.
🔹 Step 3: Configure CloudWatch Agent Installation
Under Actions, search for CloudWatch.
Select CloudWatch agent installation.
Click Edit → Enable Activate this action.
Under Parameter Store Name, enter cloudwatch-config.
Click Save action.
✅ Post-launch action is now enabled! The CloudWatch Agent will be installed automatically after a test or cutover instance is launched.

3️⃣ Modify Server Launch Settings
🔹 Step 1: Disable Instance Right-Sizing
AWS MGN automatically selects an EC2 instance type based on my source server profile.
For cost optimization, I will disable right-sizing and set my own instance type.

📌 To disable right-sizing:

1.Navigate to AWS Console → Application Migration Service.
2.Select my source server → Click Launch settings tab.
3.Click Edit in the General launch settings section.
4.Set Instance type right sizing to Off.
5.Click Save settings.

🔹 Step 2: Modify EC2 Launch Template
📌 Now, I will customize my EC2 launch template to:
- **Assign a specific subnet.
****Set instance type to t3.micro.
****Create a new security group for web access.
****Enable public IP assignment.
  
📌 To modify the EC2 Launch Template:
1.In Launch settings, click Modify under EC2 Launch Template.
2.Click Modify again when prompted.
3.Update the following settings:

🛠 Instance Type
- **Instance type → t3.micro.
- 
🌐 Networking Configuration
- **Subnet → TargetVPC-public-a.
- **Firewall (Security Groups) → Create a new security group.
    - **Security Group Name → MigratedWebServer-SG.
    - **Description → Allow HTTP from anywhere.
- **Inbound Rule:
    - **Type → HTTP
    - **Source → 0.0.0.0/0 (Allow public access)
🔹 Advanced Networking
- **Auto-assign public IP → Enable.
🔹 Tags
- **Name → Webserver.
🔹 IAM Role
- **Instance profile → migration-workshop-source-template-EC2InstanceProfile-XXX.
4.Click Create template version.
5.Copy the Launch Template ID → Click View launch templates.
6.Select the newly created template → Click Actions → Set default version.
7.Choose the latest version (e.g., Version 3) → Click Set as default version.
✅ EC2 Launch Template is now configured!

4️⃣ Verify Migration Readiness
📌 To confirm that my server is ready for testing:

1.Navigate back to AWS Console → Application Migration Service.
2.Under Source servers, my Migration lifecycle should be Ready for testing.
3.Data replication status should be Healthy.
✅ If everything looks good, I am now ready to test the migration!
➡️ **Proceed to Test Migration 🚀](./launch-test-instance.md)**
