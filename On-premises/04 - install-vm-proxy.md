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