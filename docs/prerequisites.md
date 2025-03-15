# 🛠️ Prerequisites for AWS Migration  

Before starting the migration process, I need to configure **AWS Migration Hub** and verify **IAM credentials** to ensure a smooth discovery and migration tracking process.

---

## **1️⃣ Set AWS Migration Hub Home Region**  

AWS Migration Hub **home Region** must be set so that all discovery, planning, and migration data is stored in a centralized location. This ensures that my migration activities are properly tracked.

### **Steps to Set the Home Region:**
1️⃣ Log into the **AWS Console** and navigate to **AWS Migration Hub**.  
2️⃣ From the **left menu**, select **Settings**.  
3️⃣ Under **Choose a Region**, select **US West (Oregon)** from the drop-down menu.  
4️⃣ **Enable** `Automatic redirect to home Region` to ensure future requests go to the selected region.  
5️⃣ Click **Confirm home Region** to apply the changes.  

📌 *This ensures all my migration tracking happens in a single AWS Region.*  

---

## **2️⃣ Verify IAM Credentials for AWS ADS**  

To install the **AWS Application Discovery Service (ADS) Agent** on my **Source-Webserver** and **Source-DBServer**, I need valid **AWS IAM credentials** with the appropriate permissions to communicate with AWS ADS APIs.

✅ **Retrieve IAM credentials** from **AWS IAM Console**  
✅ Ensure permissions for **AWS Application Discovery Service APIs** are assigned  

---

## **✅ Next Steps**  
➡️ **[Discover and Analyze My Environment](discovery-and-analysis.md)**  

