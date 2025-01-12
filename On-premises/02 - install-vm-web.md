## Install and configure VM-WEB

```
$vmName = "SRV-WEB"
$vmPath = "E:\VMS\SRV-WEB"
$vhdxPath = "$vmPath\$vmName.vhdx"
$secondaryVhdxPath = "$vmPath\$vmName-Secondary.vhdx"
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