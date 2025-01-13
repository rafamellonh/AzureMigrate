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

## Configure Proxy Server

* Conect to server using SSH.

* Install apache and enable support HTTPS.

```
sudo apt install -y apache2

sudo systemctl start apache2

sudo systemctl status apache2

sudo systemctl enable apache2


```

* Configure firewall : 

```
sudo ufw allow "Apache Full"
sudo ufw allow 22
sudo ufw enable

```

* Enable HTTPS

```
sudo apt install -y openssl
sudo a2enmod ssl
sudo systemctl restart apache2


```

* Create a VirtualHost for the site.

``` 
sudo vim /etc/apache2/sites-available/rafaelmellonh.conf

```
* Configure the file rafaelmellonh.conf and set the IP of SRV-WEB to do the redirection

```

<VirtualHost *:443>
    ServerName rafaelmellonh.com.br

    # Ativar SSL
    SSLEngine on
    SSLCertificateFile /etc/ssl/rafaemellonh/rafaelmellonh.crt
    SSLCertificateKeyFile /etc/ssl/rafaemellonh/rafaelmellonh.key
    SSLCertificateChainFile /etc/ssl/rafaemellonh/rafaelmellonh-chain.crt

    ################################################
    ### Proxy para o IP 192.168.1.150  (SRV-WEB)####
    ################################################

    ProxyPreserveHost On
    ProxyPass / http://192.168.1.150/
    ProxyPassReverse / http://192.168.1.150/

    # Logs 
    ErrorLog ${APACHE_LOG_DIR}/rafaelmellonh_error.log
    CustomLog ${APACHE_LOG_DIR}/rafaelmellonh_access.log combined
</VirtualHost>

<VirtualHost *:80>
    ServerName rafaelmellonh.com.br

    # Redirecionar HTTP para HTTPS
    Redirect permanent / https://rafaelmellonh.com.br/

    # Logs de acesso e erro para HTTP
    ErrorLog ${APACHE_LOG_DIR}/rafaelmellonh_error_http.log
    CustomLog ${APACHE_LOG_DIR}/rafaelmellonh_access_http.log combined
</VirtualHost>


```

* You can configure the certificates too, put the certificates if you are going to use them :

```
    SSLCertificateFile /etc/ssl/rafaemellonh/rafaelmellonh.crt
    SSLCertificateKeyFile /etc/ssl/rafaemellonh/rafaelmellonh.key
    SSLCertificateChainFile /etc/ssl/rafaemellonh/rafaelmellonh-chain.crt
    
```

* After to configure the file and put your certificates you must reload the apache and enable the site

```
sudo a2ensite rafaelmellonh.conf
sudo systemctl reload apache2

```

* Enable the mods for the proxy

```
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_ajp
sudo a2enmod rewrite
sudo a2enmod headers
sudo a2enmod proxy_balancer
sudo a2enmod lbmethod_byrequests
sudo systemctl restart apache2
```


* You can configure DNS in host.conf on your Hyper-V server or other computer to test access using the FQDN.
* On Windows, open Notepad as administrator and click on file and navigate to c:\Windows\System32\drivers\etc

![](/On-premises/img-on/linux-001.png)

* Open the file hosts and configure the IP proxy and website DNS and to save

![](/On-premises/img-on/linux-002.png)