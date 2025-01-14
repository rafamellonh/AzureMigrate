## Cloud Infrastructure

* Now we can create the infrastructure that we will use in Azure

* Design of our infrastructure :

![](/Cloud/img-cloud/cloud-infra001.png)

* You can open Azure Portal and Create a resource group

* Now, create the all Vnets and SubNets

## Create and configure Virtual Networks

* Select Virtual Networks and click on Create

![](/Cloud/img-cloud/cloud-infra06.png)

* Complete the fields with your information as shown in the images

![](/Cloud/img-cloud/cloud-infra002.png)

![](/Cloud/img-cloud/cloud-infra03.png)

![](/Cloud/img-cloud/cloud-infra04.png)

![](/Cloud/img-cloud/cloud-infra05.png)

* Review and Create

* Now we can repeat for other Vnets

![](/Cloud/img-cloud/cloud-infra07.png)

* Create NSG and link with vnets only to VNET-RM-WEB (SUB-WEB and SUB-DB), set your tag and Review and Create

![](/Cloud/img-cloud/cloud-infra08.png)

* Link subnet in NSG

![](/Cloud/img-cloud/cloud-infra09.png)

* Create peerings, go to the VNET-HUB and select Peerings, after select ADD

![](/Cloud/img-cloud/cloud-infra10.png)

![](/Cloud/img-cloud/cloud-infra11.png)
