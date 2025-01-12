## Install and configure VM-PROXY

```
$vmName = "SRV-PROXY"
$vmPath = "E:\VMS\SRV-PROXY"
$vhdxPath = "$vmPath\$vmName.vhdx"
$memorySize = 2GB
$vCpuCount = 2
$diskSizePrimary = 127GB
$isoPath = "E:\Ubuntu.iso"


New-VHD -Path $vhdxPath -SizeBytes $diskSizePrimary -Dynamic

New-Item -Path $vmPath -ItemType Directory -Force

New-VM -Name $vmName -MemoryStartupBytes $memorySize -Generation 1 -VHDPath $vhdxPath -Path $vmPath -SwitchName "VswitchExterne"

Set-VMProcessor -VMName $vmName -Count $vCpuCount

Add-VMDvdDrive -VMName $vmName -Path $isoPath


```

## - Install Ubuntu

* Select English

![](/On-premises/img-on/install-ubuntu01.png)


* Select Update to the new installer

![](/On-premises/img-on/install-ubuntu02.png)

* Select Done

![](/On-premises/img-on/install-ubuntu03.png)

* Select Done

![](/On-premises/img-on/install-ubuntu04.png)

* Select Done

![](/On-premises/img-on/install-ubuntu05.png)

* Select Done

![](/On-premises/img-on/install-ubuntu06.png)

* Select Done

![](/On-premises/img-on/install-ubuntu07.png)

* Select Done

![](/On-premises/img-on/install-ubuntu08.png)

* Select continue

![](/On-premises/img-on/install-ubuntu09.png)

* Complete the fields and done      

![](/On-premises/img-on/install-ubuntu10.png)

* Select continue      

![](/On-premises/img-on/install-ubuntu11.png)

* Select Install OpenSSH Server and done      

![](/On-premises/img-on/install-ubuntu12.png)

 Select done and wait to finish the installation

![](/On-premises/img-on/install-ubuntu13.png)