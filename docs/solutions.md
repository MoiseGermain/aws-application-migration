# **🔹 Solutions**

## **📌 Overview**
This section provides complementary **automation scripts** to streamline the implementation of the **Replatform - AWS Database Migration Service (DMS)** and **Rehost - AWS Application Migration Service (MGN)** modules. The automation leverages **Infrastructure as Code (IaC)** using **HashiCorp Terraform**.

By utilizing these scripts, you can **skip directly** to the modules focused on modernization strategies, such as:
- **Managed Container Services** → [Replatform - Amazon Elastic Container Service (ECS)](./ecs-replatform.md)
- **Managed Platform Services** → [Replatform - AWS Elastic Beanstalk (EB)](./elastic-beanstalk-replatform.md)

---

## **🔹 Requirements**
Before running the automation, ensure the following prerequisites have been met:

1️⃣ **AWS Application Migration Service (MGN) has been initialized**  
   - See [Appendix: Requirement 1](./appendix.md#requirement-1)

2️⃣ **AWS Database Migration Service (DMS) has been initialized**  
   - See [Appendix: Requirement 2](./appendix.md#requirement-2)

3️⃣ **A Cloud9 Environment has been provisioned**  
   - See [Appendix: Requirement 3](./appendix.md#requirement-3)

If these steps haven't been completed, refer to the **Appendix** section for detailed instructions.

---

## **🔹 Prepare the Environment**
Inside your **AWS Cloud9 terminal console**, download the automation scripts using the following commands:

```bash
curl -O https://static.us-east-1.prod.workshops.aws/public/0946f21b-1851-45cf-b197-69bc5bea9d6c/static/packages/amww-latest.zip
unzip amww-latest.zip
```
🖥 Cloud9 IDE
Ensure you are inside the Cloud9 environment before proceeding.

🔹 Execute the Migration
Run the main script to orchestrate all migration activities in a single step:
```bash
cd ./application-migration-workshop-walkthrough
./run_all.sh
```
⏳ Estimated Time: ~65 minutes
🚀 Time to grab a coffee while the process completes!

🔹 Final Steps
Once the script finishes, complete the final configuration for your application:

📌 Reconfigure the rehosted application server to use the replatformed database

See: Rehost - AWS Application Migration Service (MGN) > Configure Application
