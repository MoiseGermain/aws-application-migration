Review Deployed Environment
Overview
This project showcases an end-to-end AWS migration strategy for moving workloads from an on-premises data center to AWS. The deployment follows AWS best practices to ensure scalability, security, and high availability.

The source environment simulates an on-premises workload, while the target environment is built following AWS Landing Zone principles to support a production-ready migration.

Source Environment
In real-world scenarios, source environments are typically on-premises data centers with virtualized infrastructure (e.g., VMware, Hyper-V). For this project, the source environment is simulated within AWS using a dedicated VPC named SourceVPC, mimicking an on-prem setup.

Source Workload Components
Application Server (Source-Webserver)

Hosts an eCommerce Web Application (WordPress + WooCommerce)
Runs on PHP 7.x
Deployed on Amazon Linux
Database Server (Source-DBServer)

Uses self-managed MySQL 5.7.x
Runs on Amazon Linux
Accessing the Source Application
The deployed application can be accessed via WebServerDNSName, which can be found in the AWS CloudFormation Outputs. Navigating to this DNS in a browser over HTTP will load the sample eCommerce site.

Target Environment
A well-architected migration involves transitioning workloads to a secure, scalable, and highly available AWS environment. In this project, the target environment follows AWS Landing Zone architecture principles.

TargetVPC Configuration
Deployed across two Availability Zones (AZs) for high availability
Uses private subnets for application and database tiers
Integrated with IAM roles and security groups for controlled access
Current Target Environment State
At this stage, the TargetVPC is mostly empty, ready to be populated as part of the migration process. Resources will be provisioned dynamically based on the selected migration strategy.

Next Steps
➡️ Deploy the Migration Strategy
➡️ Troubleshoot Issues
