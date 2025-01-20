## Install and configure VM-SQL

```
$vmName = "SRV-SQL"
$vmPath = "E:\VMS\SRV-SQL"
$vhdxPath = "$vmPath\$vmName.vhdx"
$memorySize =4GB
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


## After installation, configure the OS

* Rename the VM and restart:

```
Rename-Computer -Newname "SRV-SQL"

```

## Download and Installation of Microsoft SQL Server Express

[Microsoft® SQL Server® 2022](https://learn.microsoft.com/en-us/sql/sql-server/install/instance-configuration?view=sql-server-ver16)  


* Open ports on firewall

```
New-NetFirewallRule -DisplayName "SQLServer default instance" -Direction Inbound -LocalPort 1433 -Protocol TCP -Action Allow
New-NetFirewallRule -DisplayName "SQLServer Browser service" -Direction Inbound -LocalPort 1434 -Protocol UDP -Action Allow

```

* [Microsoft® SQL Server® 2022 Express](https://download.microsoft.com/download/5/1/4/5145fe04-4d30-4b85-b0d1-39533663a2f1/SQL2022-SSEI-Expr.exe)  

* Open Edge and download the installer.

* Execute SQL2022-SSEI-Expr.exe

* Select Custom

![](/On-premises/img-on/install-sql01.png)

* Select Accept

![](/On-premises/img-on/install-sql02.png)

* Select Install

![](/On-premises/img-on/install-sql03.png)

* Select New Sql Server Standalone installation ...

![](/On-premises/img-on/install-sql04.png)

* Check the box and Next and next

![](/On-premises/img-on/install-sql05.png)

* Select next

![](/On-premises/img-on/install-sql06.png)

* UnCheck Azure Extension for SQL Server and next

![](/On-premises/img-on/install-sql07.png)

* Select next

![](/On-premises/img-on/install-sql08.png)

* Select Default instance and next

![](/On-premises/img-on/install-sql09.png)

* Select next

![](/On-premises/img-on/install-sql10.png)

* Select Mixed Mode and set the password and click Add Current User and after click next

![](/On-premises/img-on/install-sql11.png)

* Select close

![](/On-premises/img-on/install-sql12.png)

* After to finish, open SQL Server Configuration Manager to enable TCP/IP
* Select SQL Server Network Configuration and after Protocols for MSQLSERVER. Right click TCP/IP and enable

![](/On-premises/img-on/install-sql13.png)
