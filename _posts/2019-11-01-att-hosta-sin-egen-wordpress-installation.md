---
id: 26054
title: Sätta upp en VPS server för WordPress hosting
date: 2019-11-01T14:02:10+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=26054
permalink: /2019/11/01/att-hosta-sin-egen-wordpress-installation/
timeline_notification:
  - "1572616933"
image: /wp-content/uploads/2019/11/server-1235959_1280-1200x800.jpg
categories:
  - Hosting av wordpress
tags:
  - Digitalocean
  - hosting
  - Ubuntu
  - Wordpress
---
Välkommen till det första inlägget i serien om **Att hosta sin egna WordPress-Installation** där jag guidar dig genom processen att bygga en komplett server för att hysa dina WordPress-webbplatser. Jag kommer att börja redan från början och beskriva det fullständiga tillvägagångssättet som jag personligen gör för att bygga en ny server som är lätt att konfigurera, säkra, och optimerad för WordPress-prestanda samt skalbar för små till medelstora webbplatser. 

Servern kommer att utformas för åtkomst av en enskild användare. Därför kommer denna vägledning inte att vara lämplig för en delad servermiljö, utan är idealisk för personliga sajter. Beroende på det virtuella serverpaket du väljer, kommer den här vägledning att vara anpassad för att hantera flera webbplatser på en enda server.

I den här vägledningen kommer jag att använda en **[Di](https://m.do.co/c/430bb99817f4)****[gitalOcean](https://m.do.co/c/430bb99817f4)** (länken ger dig 50 USD att spendera gratis under 30 dagar men även mig 25 USD som tack för att du blev kund hos DigitalOcean.) **1GB-droplet** som kostar 48 SEK/månad, men du kan också välja [Linode](https://www.linode.com), [Amazon Lightsail](https://aws.amazon.com/lightsail/) eller en av de många andra virtuella serverleverantörerna. Oavsett vem du väljer så är stegen som följer i denna vägledning väldigt lika. 

Så låt oss börja bygga din nya server utan att spilla allt för mycket tid!

Läs mer om att [välja Linux-distrubition](#) i del två.