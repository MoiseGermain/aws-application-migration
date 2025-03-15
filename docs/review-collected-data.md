# Review Collected Data

AWS Application Discovery Service (ADS) provides system performance data, including average and peak utilization. This data helps with **Total Cost of Ownership (TCO)** analysis and migration planning. The **Discovery Agent** collects **detailed time-series system performance data**, **network dependencies**, and **running processes**, allowing you to group related servers as applications.

In this section, I will review the data discovered by AWS ADS, visualize dependencies, and group servers into applications.

---

## 1️⃣ View Discovered Servers

The **Servers** page provides system configuration and performance data about each discovered server. I can view **server details**, apply **filters**, tag servers with **key-value pairs**, and **export** system information.

### **To view discovered servers:**
1. Log into the **AWS Console** and navigate to:  
   ➝ **AWS Migration Hub → Discover → Servers**  
2. The discovered servers will appear in the **server list**.

📌 *It takes approximately **15 minutes** for agents to start collecting data.*

3. Click on a server under the **Server Info** column to view details such as:
   - **OS Version**
   - **Memory & CPU Usage**
   - **Performance Metrics**
   - **Network Activity**
   - **Dependencies**
   
📌 Example **detailed view** of a discovered server:  
*(This will vary depending on the collected data.)*

---

## 2️⃣ View Network Connections

Viewing **network connections** in **AWS Migration Hub** allows me to visualize **server dependencies**. This is essential for ensuring that all required components are migrated together.

### **To visualize network dependencies:**
1. Log into the **AWS Console** and navigate to:  
   ➝ **AWS Migration Hub → Discover → Servers**  
2. Select each **server** that I want to visualize.
3. Click the **Network** tab.

📌 *Now, I will see a diagram depicting how my Web Server and DB Server are connected.*  

📌 Example **network visualization diagram**:  
*(Your visualization may vary depending on the environment.)*

---

### **Important Considerations for Production Migrations**
🔹 **For actual production migrations**, AWS recommends collecting **two to six weeks** of network connection data before using the **network diagram** to analyze established traffic patterns.

---

## 3️⃣ Grouping Servers into Applications

Certain servers **must be migrated together** to maintain application functionality. AWS Migration Hub allows me to **group discovered servers into logical applications**.

### **To group servers into a new or existing application:**
1. Log into the **AWS Console** and navigate to:  
   ➝ **AWS Migration Hub → Discover → Servers**  
2. Select the servers that I want to **group together**.
3. Click **Group as Application** to create a new group or add to an existing one.

📌 Example **Application Grouping UI**:  

---

### **(Optional) Use Filters to Select Servers**
🔹 I can **filter** and **search** for servers based on:
   - **OS Type**
   - **CPU Usage**
   - **Region**
   - **Tags**
   - **Application Role**
   
🔹 To **tag** a server:  
   - Click **Add Tag**
   - Enter a **Key** (e.g., `Environment`)
   - Enter a **Value** (e.g., `Production`)

### **To finalize the application grouping:**
1. In the **Group as Application** dialog box:
   - Select **Group as a new application**  
   - Enter **Application Name** → `WebApp`  
   - *(Optional: Add a description.)*
2. Click **Group**.

📌 *The selected servers are now part of the new **Application Group**.*

---

## 4️⃣ Review the Application Groups

To review the created **Application Groups**:
1. Log into the **AWS Console** and navigate to:  
   ➝ **AWS Migration Hub → Discover → Applications**  
2. Select the **WebApp** application to explore available options.

📌 Now, the **Application Group** provides insights into:
   - **Server Dependencies**
   - **Resource Consumption**
   - **Migration Readiness**

---

## ✅ Next Steps
➡️ [Plan Migration Strategies](../docs/migration-strategies.md)
