## Create Resources

* Here we will create the resources of Azure, Storage Account, Logs Analytics Workspace, Application Gateway and Azure Bastion.

## Create a Storage Account

* This Storage Account we will be used as a cache for our replication.

* Select Storage Account in Azure Portal and click in create, use the same region as vnets.

![](/Cloud/img-cloud/sto01.png)

* Don't change anything in advanced and Networking.

![](/Cloud/img-cloud/sto02.png)

* Don't change Encryption, complete with your TAG and click review and create and after create.

## Create a Logs Analytics Workspace

* This Workspace we will use to store server logs and inventory.

* In the Azure Portal find Logs Analytics Workspace and click in create.

![](/Cloud/img-cloud/logs01.png)

* Complete the tag and review and create.

## Create an Azure Bastion

* Search for Bastion in the Azure Portal, and click in Create

* Complete all information and click in Next, In Advanced click in Next, complete the tag and Review + Create

![](/Cloud/img-cloud/bast01.png)

## Create an Application Gateway

* Search for Application Gateway in the Azure Portal, and click in Create

* Complete all information and click in Next.

![](/Cloud/img-cloud/appgw01.png)

* In FrontEnd, click in Add New to add a new IP and configure a name and OK, Next

![](/Cloud/img-cloud/appgw02.png)

* Backend we will configure after to complete the migration, now only select Yes in Add backend pool without targets and set a name.

![](/Cloud/img-cloud/appgw03.png)

* In Configuration, select Add an Rule

![](/Cloud/img-cloud/appgw04.png)

* Configure the rule, first the Listener

![](/Cloud/img-cloud/appgw05.png)
