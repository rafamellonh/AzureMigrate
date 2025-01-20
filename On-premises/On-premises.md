# Overview

To begin this setup, we need a virtualized environment capable of running nested virtualization. This can be achieved by:

## Setting Up a VM with Hyper-V
Refer to this guide to enable nested virtualization on your host machine or virtual environment. 

[Nested virtualization](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)

## Using Hardware with Virtualization Support
Ensure your hardware supports virtualization. At a minimum, you'll need:
- **16 GB of memory**  
- **Intel Core i3 processor (or higher)**

## Virtual Machines Configuration
For this project, I’ll be using a VM with Hyper-V enabled. Within this VM, I’ll configure the following three virtual machines:
- [Hyper-V](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/01%20-%20Install-configure-hv.md)
- [VM-SQL](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/02%20-%20install-vm-sql.md) 
- [VM-WEB](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/03%20-%20install-vm-web.md) 
- [VM-PROXY](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/04%20-%20install-vm-proxy.md) 

Follow the links for detailed setup instructions for each VM.


![Infra on-premises](./On-premises/img-on/local01.png)