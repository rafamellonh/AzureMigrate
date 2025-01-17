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

* Complete the VM startup settings, similar to the first boot after installing the SRV-WEB and SRV-SQL servers.

* Wait a few minutes after the first logon and click on the link on the desktop : Azure Migrate Appliance Configuration Manager.

* On Set up prerequisite, paste the key that was generated previously and that was noted on Verification of Azure Migrate project Key and click in Verify

![](/Cloud/img-cloud/pro009.png)

* Now click in Rerun prerequisites and after Verify again.

![](/Cloud/img-cloud/pro10.png)

* Now that is possible to click in Login. Copy the code and paste in the new tab that will open, Next.

* Log in with the azure account that is being used.

![](/Cloud/img-cloud/pro011.png)

* After logon, we return to the configuration page to configure the credentials and wait for the azure app registration to complete.

![](/Cloud/img-cloud/prod012.png)

* Now, click on Add Credentials to add an administrative credential for Hyper-V. Complete with your credentials of user administrator and save

![](/Cloud/img-cloud/pro013.png)

* After, click on Add Discovery source to add the Hyper-V Server to the search. Complete with the IP of Hyper-V and the credential created before and save.

![](/Cloud/img-cloud/pro014.png)
 
* In the Step 3, turn off Disable the slider if you don't want to perform these features (you can change this later) and click in Start discovery.

![](/Cloud/img-cloud/pro015.png)

* After discovery is complete, you can validate the discovery servers in Azure. In Azure Migrate, select Servers, databases and web apps. In Assessment tools, click on the number below Discovered servers

![](/Cloud/img-cloud/pro016.png)

![](/Cloud/img-cloud/pro017.png)

* Let's create a group to carry out the migration process, in this same panel, click on Create Group

* Fill in the same information so that it uses the servers that were found in discovery and will use these servers to create assessments for them, to check prices and the best hardware configuration. Select only vms that will migrate and click Create.

![](/Cloud/img-cloud/pro018.png)

* Now create an assessment to evaluate the compatibility, performance, and costs of migrating workloads to Azure, identifying dependencies, and right-sizing resources. It helps you plan strategies, optimize resources, and prioritize migrations to ensure efficiency and cost-effectiveness. Go back to Azure Migrate painel, click on Servers, databases and web apps.

* in Discovery and assessment, click on Asses and select Azure VM

![](/Cloud/img-cloud/prod019.png)

* Choose the same information and click in Edit

![](/Cloud/img-cloud/pro020.png)

* Select features as per your need and click in save. In the next page, click in Next: Select servers to assess

![](/Cloud/img-cloud/pro021.png)

* In Create assessment, create name of asses and select your group, after click in Review and Create and after Create

![](/Cloud/img-cloud/pro021.png)