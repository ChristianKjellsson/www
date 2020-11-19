---
id: 25999
title: Perfect wordpress server
date: 2018-03-14T10:18:00+00:00
author: Christian Kjellsson
layout: post
guid: https://christiankjellsson.com/?p=25999
permalink: /2018/03/14/perfect-wordpress-server/
categories:
  - Computer
  - Snippets
---
## Konfiguera server-setup

Som root@IP-Adress satte jag hostname  
`echo "template.christiankjellsson.com"  > /etc/hostname`  
`hostname -F /etc/hostname`

Konfigurerat tidszonen  
`dpkg-reconfigure tzdata`

Uppdaterat och uppgradera mjukvara  
`apt-get update && apt-get upgrade -y`

Tagit bort onödig mjukvara  
`apt-get autoremove`

Skapat en ny användare och gett sudo rättigheter  
`adduser chefen`  
`usermod -a -G sudo chefen`

Ändrat så att root enbart kan loggas in med SSH-key  
`sudo nano /etc/ssh/sshd_config`  
`PermitRoot without-password`

Sparat ändringen  
`service ssh restart`

Logga ut som root.  
`logout`

Loggat in som chefen och lagt in min SSH-key för hata lösenord.  
`ssh chefen@IP-Adress`  
`nano .ssh/authorized_keys`

Installerat brandvägg  
`sudo apt-get install ufw`

Satt regeler  
`sudo ufw allow ssh`  
`sudo ufw allow http`  
`sudo ufw allow https`

Startat brandvägg  
`sudo ufw enable`

Dubbellkollat att där är 6 st regler  
`sudo ufw status verbose`

Installerat Fail2Ban  
`sudo apt-get install fail2ban`

Startat fail2ban  
`sudo service fail2ban start`

## Installera webserver, php och databas

### Nginx, PHP7.1 och MariaDB

Lagt till senaste versionen av Nginx repot  
`sudo add-apt-repository ppa:nginx/development -y`  
Uppdaterat mina repon på servern  
`sudo apt-get update`  
Installerat Nginx  
`sudo apt-get install nginx -y`  
Kontrollerat att jag har en relativt ny version  
`nginx -v`