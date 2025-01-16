## Azure Migrate

* Find Azure Migrate in Azure portal, select Servers, databases and webapps, and click in Create project.

![](/Cloud/img-cloud/pro001.png)

* You can select any location in geography, it's for the metadata. Select Create.

![](/Cloud/img-cloud/pro002.png)

* Now we have to options, Assessment tools and Migrations tools. Assessment tools are used to create a discovery and an inventory. With inventory, we can create a pricing.
Migrations tools are used to migrate.

* Create a Discover, in Assessment tools click in Discover and select Using appliance. 

![](/Cloud/img-cloud/pro003.png)

* Select : Yes, with Hyper-v

![](/Cloud/img-cloud/pro004.png)

* Now, complete the name of your appliance (this appliance will be a new VM in Hyper-v to discover all the servers that are being migrated, and the appliance will do the entire migration process), and click in Generate Key.  Take note of this key.

![](/Cloud/img-cloud/pro005.png)

* Now select .VHD File 12GB and click Download. (Try running directly in Hyper-v) as a vm will be created from this VHD.

![](/Cloud/img-cloud/pro006.png)

* After downloading, unzip the file and, in Hyper-V Manager, click on import Virtual Machine and select the unzipped file adn, Next

![](/Cloud/img-cloud/pro007.png)

* Next for Select Virtual Machine

* In Choose Import Type, select Register the virtual machine in-place, and Next.

* Configure Processor, select 2 of Number of virtual processors.

* In Connect Network, select the Virtual Switch created before (VswitchExterne) [01 - Install-configure-hv](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/01%20-%20Install-configure-hv.md) and Next, Finish on Summary.

* Since hyper-v only has 16G, set this VM's memory to start with 4G and use dynamic memory.

* Select VM and right-click. Select Settings, in the settings select Memory and adjust. Ok and start vm.

![](/Cloud/img-cloud/pro008.png)