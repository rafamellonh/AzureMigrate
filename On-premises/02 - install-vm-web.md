## Install and configure VM-WEB

```
$vmName = "SRV-WEB"
$vmPath = "E:\VMS\SRV-WEB"
$vhdxPath = "$vmPath\$vmName.vhdx"
$memorySize =2GB
$vCpuCount = 2
$diskSizePrimary = 127GB
$isoPath = "E:\Windows-Server-2022.iso"


New-VHD -Path $vhdxPath -SizeBytes $diskSizePrimary -Dynamic

New-Item -Path $vmPath -ItemType Directory -Force

New-VM -Name $vmName -MemoryStartupBytes $memorySize -Generation 2 -VHDPath $vhdxPath -Path $vmPath -SwitchName "VswitchExterne"

Set-VMProcessor -VMName $vmName -Count $vCpuCount

Add-VMDvdDrive -VMName $vmName -Path $isoPath


```

* Repeat step 3 of [01 - Install-configure-hv](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/01%20-%20Install-configure-hv.md)  

* Rename the VM and restart:

```
Rename-Computer -Newname "SRV-WEB"

```

## Download application and Installation IIS

 [SmartStoreNET](https://github.com/smartstore/SmartStoreNET/releases/download/3.2.2/SmartStoreNET.Community.3.2.2.zip ) 

* Open Edge and download the installer.

* Install IIS, on Server Manager select Manage and Add Roles And Features

![](/On-premises/img-on/install-iis01.png)

* Select next

![](/On-premises/img-on/install-iis02.png)

* Select next

![](/On-premises/img-on/install-iis03.png)

* Select next

![](/On-premises/img-on/install-iis04.png)

* Select Web Server (IIS)

![](/On-premises/img-on/install-iis05.png)

* Select Add Features and next

![](/On-premises/img-on/install-iis06.png)


* Select next

![](/On-premises/img-on/install-iis08.png)

* Select the options as in the image and next and install

![](/On-premises/img-on/install-iis09.png)

* Select close

![](/On-premises/img-on/install-iis10.png)

* Extract the files to ``` c:\inetpub\wwwwroot\smartstore ```. (You must have downloaded it at the beginning of the procedure)

![](/On-premises/img-on/install-iis11.png)


## Configure IIS

* Select Server Manager, Tools and select Internet Information Services IIS Manager

* In Internet Information Services IIS Manager expand SRV-WEB and Sites

* Stop Default Web Site

![](/On-premises/img-on/install-iis12.png)

* Right click on Sites and Add Website 

![](/On-premises/img-on/install-iis13.png)

* Fill in the fields as shown in the image and OK and Yes

![](/On-premises/img-on/install-iis14.png)

* Set permission on SmartStore path ``` c:\inetpub\wwwwroot\smartstore ```. Right click on SmartStore and selec Properties

![](/On-premises/img-on/install-iis15.png)

* Select Security and Edit, after sele IIS_IUSRS and check Full Control and OK, OK.

![](/On-premises/img-on/install-iis16.png)