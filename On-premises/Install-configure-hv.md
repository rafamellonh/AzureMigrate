 * Para realizarmos a instalacao, iremos utilizar o Windows Server 2022 Evaluation, download aqui : https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022

* Voce pode criar manualmente a VM ou executar o script powershell abaixo para agilizar o deploy

```
# Variáveis de configuração
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


# Criação do diretório da VM
New-Item -Path $vmPath -ItemType Directory -Force


# Criação da máquina virtual
New-VM -Name $vmName -MemoryStartupBytes $memorySize -Generation 2 -VHDPath $vhdxPath -Path $vmPath -SwitchName "vswitchExterne"

Set-VMProcessor -VMName $vmName -Count $vCpuCount
Set-VMMemory -VMName $vmName -StartupBytes $memorySize -MaximumBytes $memorySize -MinimumBytes $memorySize


# Criação e adição do disco secundário (250 GB)
Add-VMHardDiskDrive -VMName $vmName -Path $secondaryVhdxPath

# Adicionar a ISO do sistema operacional para a instalação
Add-VMDvdDrive -VMName $vmName -Path $isoPath



```

## Configure Nested Virtualization

* After to finish the installation, execute on Powershell  :

```
Set-VMProcessor -VMName "SRV-HV" -ExposeVirtualizationExtensions $true

Get-VMNetworkAdapter -VMName "SRV-HV" | Set-VMNetworkAdapter -MacAddressSpoofing On

Start-VM $vmName

```

* Apos criar vm, iremos instalar o sistema operacional

## Install Windows

* Select Next

![](/On-premises/img-on/install-hv-01.png)

* Click Install Now

![](/On-premises/img-on/install-hv-02.png)

* Select Windows Server 2022 Datacenter (Desktop Experience)

![](/On-premises/img-on/install-hv-03.png)

* Checkt the box

![](/On-premises/img-on/install-hv-04.png)

* Select Custom: Install Microsoft Server Operating System only (advanced)

![](/On-premises/img-on/install-hv-05.png)

* Select the disk and next

![](/On-premises/img-on/install-hv-06.png)

* After installation, configure the password and finish

![](/On-premises/img-on/install-hv-07.png)

## OS Configuration 

