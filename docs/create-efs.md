# **📂 Create an Amazon EFS File System**

## **📌 Overview**
Amazon Elastic File System (EFS) provides scalable file storage that integrates seamlessly with ECS tasks. In this step, I will:

✅ **Create an Amazon EFS file system**  
✅ **Configure network mount targets**  
✅ **Mount the EFS on the migrated webserver**  
✅ **Copy WordPress content to the EFS**  

---

## **🛠️ Step 1: Create an Amazon EFS File System**
📌 **I need to create an EFS that will store shared data for my web application.**

1️⃣ In the **AWS Console**, go to **Services > EFS**  
2️⃣ Click **Create file system**  
3️⃣ Enter the following values:

| Parameter             | Value                      |
|----------------------|--------------------------|
| **File system name** | `webserver-filesystem`   |
| **VPC**              | `TargetVPC`              |

4️⃣ Click **Create**  
5️⃣ In the list of file systems, click on **`webserver-filesystem`** to open its details  

📷 [**Create Elastic File System**](images/create-efs.png)

---

## **🛠️ Step 2: Configure Network Mount Targets**
📌 **I need to configure EFS to work with my VPC's private subnets.**

1️⃣ In the **EFS details page**, go to the **Network** tab  
2️⃣ Click **Manage** under **Mount targets**  
3️⃣ Remove the **2 existing mount targets**  
4️⃣ Add **2 new mount targets** with the following settings:

| Availability Zone | Subnet ID                     | Security Group |
|------------------|-----------------------------|---------------|
| `us-west-2a`    | `TargetVPC-private-a-web`   | `EFS-SG`      |
| `us-west-2b`    | `TargetVPC-private-b-web`   | `EFS-SG`      |

5️⃣ Click **Save**  

📷 [**Configure Network Mount Targets**](images/configure-mount-targets.png)

---

## **🛠️ Step 3: Retrieve the File System ID**
📌 **I need the EFS File System ID to mount the EFS on my webserver.**  

1️⃣ In the **EFS details page**, locate the **File System ID**  
2️⃣ Make a note of it for later  

🔗 **EFS DNS format:**  
file-system-id.efs.aws-region.amazonaws.com
```

📷 [**EFS File System ID**](images/efs-id.png)

---

## **🛠️ Step 4: Mount EFS on the Webserver**
📌 **Now, I will mount the EFS on my webserver and copy WordPress content to it.**  

1️⃣ Log into the **migrated webserver** using **SSH** or **Session Manager**  
2️⃣ Run the following commands:

```bash
sudo apt-get update -y
sudo apt-get install -y nfs-common
sudo mkdir /efs
```
3️⃣ Mount the EFS file system (replace FILE_SYSTEM_ID with the actual ID):
```bash
sudo mount -t nfs -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport FILE_SYSTEM_ID.efs.us-west-2.amazonaws.com:/ /efs
```
🛠️ Step 5: Copy WordPress Content to EFS
📌 I will now copy my WordPress wp-content folder to the EFS storage.
```
sudo cp -r /var/www/html/wp-content/* /efs
```
✅ At this point, my web application’s static files are stored on EFS, making it highly available.
⚠️ Troubleshooting
📌 If I encounter issues mounting the EFS, I will:

Check EFS mount logs using:
```
sudo dmesg | tail
```
Verify that EFS Security Groups allow traffic from ECS tasks
Confirm NFS utilities are installed (nfs-common)
Reference the AWS EFS Troubleshooting Guide
📷 AWS EFS Troubleshooting

📌 Next Steps
✅ EFS is now set up and mounted on the webserver.
➡️ Step 3: **[Configure AWS Systems Manager Parameter Store for Database Credentials](../docs/store-db-credentials.md)** 
