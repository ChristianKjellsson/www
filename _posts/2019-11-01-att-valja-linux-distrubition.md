---
id: 26062
title: 'Sätta upp en VPS server för WordPress hosting &#8211; Del 2'
date: 2019-11-01T15:05:03+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=26062
permalink: /2019/11/01/att-valja-linux-distrubition/
timeline_notification:
  - "1572620710"
image: /wp-content/uploads/2019/11/bandwidth-close-up-connection-1148820-1200x801.jpg
categories:
  - Hosting av wordpress
tags:
  - hosting
  - Wordpress
---
Jag kommer inte att gå in i detalj om det ursprungliga skapandet av droppar (server) eftersom [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server) har en egen handledning, men jag vill lista upp orsakerna till att jag väljer Ubuntu som min Linux-distribution. Ubuntu är en av de mest populära distributionerna för servrar och här är några skäl till varför:

  * Tungt fokuserat på användbarhet
  * Ett stort urval av paket
  * Frekventa programuppdateringar
  * Ett stort onlinecommunity som leder till mer användbara resurser 

En nackdel med att välja en distribution med frekventa programuppdateringar är att det är möjligt att det finns nya buggar och problem. Lyckligtvis har Ubuntu en LTS-version (Long Term Support), som använder paket som anses vara mer stabila. LTS-utgåvor sker vartannat år och stöds i 5 år &#8211; vilket gör dem lämpliga för produktionsservrar. I skrivande stund är den senaste versionen av LTS 18.04 (Bionic Beaver), vilket är den version jag ska välja.  
  
Med distributions- och släppversionen vald, gå vidare och skapa en ny droplet. Kom ihåg att välja en region som är närmast dina besökare. Jag skulle också rekommendera att du aktiverar alternativet &#8220;Monitoring&#8221;. <figure class="wp-block-image size-large">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image.png?w=1024" alt="" class="wp-image-26064" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image.png 1920w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-300x164.png 300w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-1024x560.png 1024w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-768x420.png 768w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-1536x840.png 1536w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-1200x656.png 1200w" sizes="(max-width: 1920px) 100vw, 1920px" /> </figure> 

<p class="has-large-font-size">
  Logga in på vår server
</p>

Låt oss logga in första gången, eftersom denna guide är för Windows-användare så kommer jag att använda mig av PuTTY.

Det finns en sjö av olika SSH-klienter för att ansluta till en server med SSH där en av de mest kända är [PuTTY](https://www.putty.org/).

<!--StartFragment--><figure class="wp-block-image size-full">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image-1.png" alt="" class="wp-image-26078" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-1.png 452w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-1-300x293.png 300w" sizes="(max-width: 452px) 100vw, 452px" /> <figcaption> Efter du har laddat ner och öppnat filen så ser det ut så här. </figcaption></figure> 

<!--EndFragment-->

Under hostname så skriver du in IP-adressen som din nyligen skapade droplet fick. I din inkorg så har du mottagit ett mail från DigitalOcean med en användare som heter root och ett tillhörande password.

I PuTTY så skriver vi in IP-adressen som vi fick under Hostname och trycker sedan på Open.<figure class="wp-block-image size-large">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image-3.png?w=452" alt="" class="wp-image-26081" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-3.png 452w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-3-300x293.png 300w" sizes="(max-width: 452px) 100vw, 452px" /> </figure> 

Efter du har tryck på Open så ska du logga in med root-användaren och sedan skriva in lösenordet som du fick i mailet. Om lösenordet är långt och besvärligt så kan du kopiera det och sedan klistra in det i PuTTY genom atta trycka på höger-musknapp.<figure class="wp-block-image size-large">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image-4.png?w=661" alt="" class="wp-image-26082" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-4.png 661w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-4-300x190.png 300w" sizes="(max-width: 661px) 100vw, 661px" /> <figcaption> Dropleten som vi skapade hos DigitalOcean ber oss nu om att logga in. </figcaption></figure> 

Efter att du har klistrat in ditt lösenord så kan du inte se att det visas något. Lösenordet är gömt. Tryck bara på Enter-knappen efter du har klistrat in det.<figure class="wp-block-image size-large">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image-5.png?w=877" alt="" class="wp-image-26083" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-5.png 877w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-5-300x181.png 300w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-5-768x464.png 768w" sizes="(max-width: 877px) 100vw, 877px" /> <figcaption>Inloggad i servern vi precis har skapat.</figcaption></figure> 

Nu är vi inloggade på ny Ubuntu-server och kan i [del tre börja säkra upp den.](http://satta-upp-en-vps-server-for-wordpress-hosting-del-3-sakra-upp-ubuntu)