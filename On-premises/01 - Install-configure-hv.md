* To perform the installation, we will use Windows Server 2022 Evaluation, download here: : https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022

* You can manually create the VM or run the powershell script below to speed up the deployment.

## 1 - Create VM to use as Hyper-V

```
# Configuration variables
$vmName = "SRV-HV"
$vmPath = "D:\VMS\SRV-HV"
$vhdxPath = "$vmPath\$vmName.vhdx"
$secondaryVhdxPath = "$vmPath\$vmName-Secondary.vhdx"
$memorySize = 16GB
$vCpuCount = 4
$diskSizePrimary = 127GB
$diskSizeSecondary = 250GB
$isoPath = "D:\ISO\Windows Server\Windows-Server-2022.iso"  # Caminho para a ISO do sistema operacional

#Creating disks
New-VHD -Path $vhdxPath -SizeBytes $diskSizePrimary -Dynamic
New-VHD -Path $secondaryVhdxPath -SizeBytes $diskSizeSecondary -Dynamic

New-Item -Path $vmPath -ItemType Directory -Force

New-VM -Name $vmName -MemoryStartupBytes $memorySize -Generation 2 -VHDPath $vhdxPath -Path $vmPath -SwitchName "vswitchExterne"

Set-VMProcessor -VMName $vmName -Count $vCpuCount
Set-VMMemory -VMName $vmName -StartupBytes $memorySize -MaximumBytes $memorySize -MinimumBytes $memorySize

Add-VMHardDiskDrive -VMName $vmName -Path $secondaryVhdxPath

Add-VMDvdDrive -VMName $vmName -Path $isoPath



```

## 2 - Configure Nested Virtualization

* After to finish the installation, execute on Powershell  :

```
Set-VMProcessor -VMName "SRV-HV" -ExposeVirtualizationExtensions $true

Get-VMNetworkAdapter -VMName "SRV-HV" | Set-VMNetworkAdapter -MacAddressSpoofing On

Start-VM "SRV-HV"

```

* After creating the vm, we will install the operating system

## 3 - Install Windows

* Select Next

![](/On-premises/img-on/install-hv-01.png)

* Click Install Now

![](/On-premises/img-on/install-hv-02.png)

* Select Windows Server 2022 Datacenter (Desktop Experience)

![](/On-premises/img-on/install-hv-03.png)

* Check the box

![](/On-premises/img-on/install-hv-04.png)

* Select Custom: Install Microsoft Server Operating System only (advanced)

![](/On-premises/img-on/install-hv-05.png)

* Select the disk and next

![](/On-premises/img-on/install-hv-06.png)

* After installation, configure the password and finish

![](/On-premises/img-on/install-hv-07.png)

## 4 - OS Configuration 

* login and let's adjust the vm name and install Hyper-V. Open Powershell and execute the command :

```
Rename-Computer -Newname "SRV-SQL"

Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart

```

* Configure secondary disk, check disk number with command: ``` get-disk ```. The disk to configure is 250G in size


```

Set-Disk -Number 1 -IsOffline $false

Initialize-Disk -Number 1 -PartitionStyle GPT

New-Partition -DiskNumber 1 -UseMaximumSize -DriveLetter E

Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "VMS" -Confirm:$false

```

* Configure a new virtual switch. Check the name of your Network Adapter :  ```  Get-NetAdapter  ```

```
New-VMSwitch -Name "VswitchExterne" -NetAdapterName "Ethernet" -AllowManagementOS $true

```

## 5 - Install all VMS

* Download ISO's 
    * [Windows Server 2022 ](https://software-static.download.prss.microsoft.com/sg/download/888969d5-f34g-4e03-ac9d-1f9786c66749/SERVER_EVAL_x64FRE_en-us.iso) 
    * [Ubuntu](https://mirror.hep.gg/ubuntu-releases/24.04.1/ubuntu-24.04.1-live-server-amd64.iso) 

* Now we are install the 3 VMS, we can open the powershell on Hyper-V and to execute the commands : 


* [VM-SQL ](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/02%20-%20install-vm-sql.md) 
* [VM-WEB ](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/03%20-%20install-vm-web.md) 
* [VM-PROXY ](https://github.com/rafamellonh/AzureMigrate/blob/main/On-premises/04%20-%20install-vm-proxy.md) 