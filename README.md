# Azure Migration Project

## Overview
This project aims to migrate two virtual machines (**VM-SQL** and **VM-WEB**) from an on-premises **Hyper-V** environment to **Microsoft Azure**. Additionally, the reverse proxy currently configured on a virtual machine will be replaced with an **Azure Application Gateway**, providing enhanced security, scalability, and performance for traffic management.

---

## Current Environment
### On-Premises Infrastructure
- The current environment is based on VMs managed by **Hyper-V**:
  - **VM-SQL:** Hosts the SQL Server database.
  - **VM-WEB:** Hosts the website using IIS (Internet Information Services).
  - **VM-PROXY:** Acts as the reverse proxy, hosted on an Ubuntu server.
- Communication between components occurs within a local network.

### Challenges of the Current Infrastructure
- Dependence on physical hardware with limited resources.
- Manual maintenance and complex management.
- Lack of scalability and high availability.

---

## Migration Plan
### 1. Project Scope
- Migrate the **VM-SQL** and **VM-WEB** VMs to Azure using **Azure Virtual Machines**.
- Replace the reverse proxy hosted on **VM-PROXY** with an **Azure Application Gateway**, integrated with the Azure environment.

### 2. Project Steps
#### Planning and Analysis
- Assess the configurations and requirements of the VMs (resources, operating system, and applications).
- Identify dependencies between **VM-SQL**, **VM-WEB**, and the proxy.
- Size the required resources in Azure.

#### Azure Environment Setup
- Create Azure VMs to host **VM-SQL** and **VM-WEB**:
  - **VM-SQL:** Configure a virtual machine with SQL Server support, ensuring compatibility with existing data.
  - **VM-WEB:** Configure a virtual machine for IIS, replicating the site settings.
- Configure the **Azure Application Gateway** to replace the reverse proxy, with routing rules and integrated SSL.

#### Migration and Testing
- Migrate the content from the on-premises VMs to the new Azure VMs using tools such as **Azure Migrate**.
- Test connectivity between **VM-WEB**, **VM-SQL**, and the Application Gateway.
- Conduct load and security testing to validate the functionality in Azure.

#### Cutover and Post-Migration
- Redirect traffic to the new Azure environment during the migration window.
- Monitor performance and address potential issues using **Azure Monitor** and **Log Analytics**.

---

## Migration Benefits
1. **Scalability:** Azure VMs can be dynamically scaled to accommodate business growth.
2. **High Availability:** Azure services offer SLAs of 99.95% or higher.
3. **Advanced Security:** **Application Gateway** includes DDoS protection and centralized SSL management.
4. **Simplified Management:** Reduced dependency on physical hardware and improved automation for VM management.
5. **Modernized Infrastructure:** A modern infrastructure ready for future integrations and expansions.

---

## Next Steps
1. Review the current VM configurations and dependencies.
2. Create a detailed schedule for migration and validation.
3. Begin the implementation of the Azure environment.
