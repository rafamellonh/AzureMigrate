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