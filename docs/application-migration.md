# 🚀 **Application Migration**

## **🔹 Application Migration Strategies**
A **migration strategy** defines how an application is transitioned from an on-premises environment to the AWS Cloud. AWS outlines **seven key migration strategies**, but the most common patterns include:

### **🔹 Common Migration Strategies**
1️⃣ **Rehost (Lift and Shift)**  
   - Move applications **without modifications** to AWS.  
   - **Best for:** Rapid migrations with minimal changes.  

2️⃣ **Replatform (Lift, Tinker, and Shift)**  
   - Migrate applications **with minor optimizations** to leverage AWS capabilities.  
   - **Best for:** Reducing costs, improving efficiency, and adopting cloud-native features.  

3️⃣ **Repurchase (Drop and Shop)**  
   - Replace existing software with **cloud-based SaaS solutions**.  
   - **Best for:** Moving from legacy applications to modern cloud-native software.  

4️⃣ **Refactor (Re-architect)**  
   - Completely re-architect applications to use **cloud-native services**.  
   - **Best for:** Long-term scalability, agility, and cost efficiency.  

🔗 **[View Migration Strategies Diagram](assets/migration-strategies-diagram.png)**  

---

## **🔹 Migration Approaches in This Project**
This project focuses on **three key strategies**:

🔹 **Option 1: Rehost with AWS Application Migration Service (MGN)**  
   - Ideal for **simple lift-and-shift migrations** with minimal disruption.  

🔹 **Option 2: Rehost with AWS MGN for Large Migrations**  
   - Uses **Applications and Waves** to manage migrations involving multiple servers.  

🔹 **Replatforming with AWS Managed Services**  
   - **Amazon ECS**: Run applications in containers with AWS-managed infrastructure.  
   - **AWS Elastic Beanstalk**: Deploy applications on fully managed platforms.  

---

## **📌 Important Note**
💡 **Follow the order of modules!**  
- **Replatforming modules depend on completing Rehosting first.**  
- Choose **either Option 1 or Option 2 for Rehosting**, but **not both**.  

🔜 **[Proceed to Rehosting with AWS MGN](./rehost-mgn.md)**  
