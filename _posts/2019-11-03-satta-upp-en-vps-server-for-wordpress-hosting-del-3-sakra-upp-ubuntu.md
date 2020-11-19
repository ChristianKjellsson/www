---
id: 26096
title: Sätta upp en VPS server för WordPress hosting – Del 3 säkra upp Ubuntu
date: 2019-11-03T15:20:36+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=26096
permalink: /2019/11/03/satta-upp-en-vps-server-for-wordpress-hosting-del-3-sakra-upp-ubuntu/
timeline_notification:
  - "1572794441"
image: /wp-content/uploads/2019/11/security-265130_1920-1200x800.jpg
categories:
  - Hosting av wordpress
tags:
  - Brandvägg
  - Fail2Ban
  - SSH
  - UFW
---
I denna del av hur man sätter upp en VPS server för att hysa en WordPress-installation så kommer jag att gå igenom de absolut första åtgärder man tar när man har fått tillgång till servern. Inlägget kommer bland annat att gå igenom hur vi sätter upp en användare med privilegerade rättigheter men även hur man installerar en brandvägg och får den konfigurerat.

Detta är en artikel som tillhör en artikelserie. Övriga delar hittar du här.

  * [Sätta upp en VPS server för WordPress hosting – Del 1](https://christiankjellsson.com/2019/11/01/att-hosta-sin-egen-wordpress-installation/)
  * [Sätta upp en VPS server för WordPress hosting – Del 2 Att välj Linux-distrubtition](https://christiankjellsson.com/2019/11/01/att-valja-linux-distrubition/) 

## Ställ in värdnamnet på servern

<span class="tlid-translation translation" lang="sv"><span title="">Nu när du är inloggad på servern, låt oss ange ett värdnamn som är ett fullt kvalificerat domännamn (FQDN).</span> <span class="" title="">Värdnamnet ska vara unikt men kräver inte någon relation till de webbplatser som kommer att vara värd. Till exempel namnger folk ofta sina servrar efter astronomiska objekt.</span> <span class="" title="">Att korrekt ställa in värdnamnet och FQDN kommer att göra anslutningen till din server mycket enklare i framtiden eftersom du inte kommer att komma ihåg IP-adressen varje gång.</span></span>

 <span class="tlid-translation translation" lang="sv"><span class="" title="">För att ställa in värdnamnet, utfärda följande kommandon och tryck enter efter varje kommando.</span></span>

`echo "moon.christiankjellsson.com" > /etc/hostname`

`hostname -F /etc/hostname`

<span class="tlid-translation translation" lang="sv"><span title="">För att ansluta till servern med ditt värdnamn måste du uppdatera ditt domännamns DNS-inställningar.</span> <span class="" title="">Logga in på din DNS-kontrollpanel och skapa en ny A-post och här behöver du logga in på hemsidan där du köpte din domän t ex <a href="https://www.loopia.se/">Loopia</a> eller <a href="https://www.name.com">name.com</a>.<br /></span></span>

Under inställningarna så väljer du att A Record ska pekas mot serverns IP-adress. Det vill säga att moon.christiankjellsson.com ska matcha serverns IP-adress.

## Ställa in tidszon

<span class="tlid-translation translation" lang="sv"><span class="" title="">För att servern ska köras i din lokala tidszon måste du konfigurera tzdata-paketet, vilket kommer att säkerställa att systemloggfilerna visar rätt datum och tid.</span> <span title="">Följande kommando tillåter dig att konfigurera tzdata-paketet:</span></span>

    dpkg-reconfigure tzdata

<span class="tlid-translation translation" lang="sv"><span class="" title="">En enkel GUI visas så att du kan välja ditt geografiska område och tidszon:</span></span><img class="alignnone size-full wp-image-26100" src="https://christiankjellssoncom.files.wordpress.com/2019/11/2019-11-02_12h34_56.png" alt="2019-11-02_12h34_56" width="877" height="530" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/2019-11-02_12h34_56.png 877w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/2019-11-02_12h34_56-300x181.png 300w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/2019-11-02_12h34_56-768x464.png 768w" sizes="(max-width: 877px) 100vw, 877px" />

<span class="tlid-translation translation" lang="sv"><span class="" title="">När det är klart kommer den nyligen valda tidszonen att visas tillsammans med aktuell tid och datum:</span></span><img class="alignnone size-full wp-image-26102" src="https://christiankjellssoncom.files.wordpress.com/2019/11/2019-11-02_12h36_32.png" alt="2019-11-02_12h36_32" width="877" height="530" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/2019-11-02_12h36_32.png 877w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/2019-11-02_12h36_32-300x181.png 300w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/2019-11-02_12h36_32-768x464.png 768w" sizes="(max-width: 877px) 100vw, 877px" />

## <span class="tlid-translation translation" lang="sv"><span class="" title="">Installera programuppdateringar</span></span>

<span class="tlid-translation translation" lang="sv"><span class="" title="">Även om du bara har tillhandahållit din nya server är det troligt att vissa programvarupaket är inaktuella.</span> <span class="" title="">Låt oss se till att du använder den senaste programvaran genom att dra in uppdaterade paketlistor:</span></span>

    apt-get update

När det är klart, låt oss uppdatera alla de för närvarande installerade paketen. Du kommer att uppmanas med hur mycket utrymme uppdateringarna kommer att ta och tryck på Enter kommer att starta processen följt av ett Y för att installera uppdateringarna:

    apt-get upgrade

När uppgraderingarna har slutförts kommer du att se vilka paket som har installerats och även vilka paket som inte längre krävs av systemet.

Ta gärna bort de föråldrade paketen genom att utfärda följande kommando:

    apt-get autoremove

## <span class="tlid-translation translation" lang="sv"><span title="">Skapa en ny användare</span><br /></span>

<span class="tlid-translation translation" lang="sv"><span title="">Det är dags att lägga till en ny användare på din server.</span> <span title="">Det finns två skäl till detta:</span></span>

<li style="list-style-type:none;">
  <ol>
    <li>
      Senare i den här tutorialen kommer du att inaktivera root-inloggning, vilket innebär att du behöver ett annat användarkonto för att komma åt din server.
    </li>
    <li>
      Rotanvändaren innehåller mycket breda privilegier som gör att du kan utföra potentiellt förstörande kommandon.Därför rekommenderas det att skapa ett nytt användarkonto med mer begränsade behörigheter för den dagliga användningen.Den här nya användaren läggs till i sudo-gruppen så att du kan utföra kommandon som kräver ökade behörigheter, men bara när det behövs.
    </li>
  </ol>
</li>

<span class="" title="">Skapa först den nya användaren, jag har valt att döpa min användare till mitt efternamn:</span>

<pre class="wp-block-code"><code>adduser kjellsson</code></pre><figure class="wp-block-image size-large">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image-6.png?w=877" alt="" class="wp-image-26107" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-6.png 877w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-6-300x181.png 300w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-6-768x464.png 768w" sizes="(max-width: 877px) 100vw, 877px" /> </figure> 

Nu måste du lägga till den nya användaren i sudo-gruppen: 

<pre class="wp-block-code"><code>usermod -a -G sudo kjellsson</code></pre>

Kontrollera nu att ditt nya konto fungerar genom att logga ut från din nuvarande SSH-session och initiera ett nytt: 

<pre class="wp-block-preformatted"><code>logout</code> </pre>

Logga sedan in med ditt nya konto mot domänen.

<pre class="wp-block-preformatted">ssh kjellsson@moon.christiankjellsson.com</pre>

## Konfigurera SSH

Nu när din nya användare är skapad, är det dags att ytterligare säkra servern genom att konfigurera SSH. Det första du ska göra är att inaktivera root-inloggning, vilket som namnet antyder inte längre låter dig logga in på servern via SSH med standard root-användaren. Öppna SSH-konfigurationsfilen med nano (lägg märke till att du använder sudo för att höja privilegierna för detta kommando):

<pre class="wp-block-preformatted">sudo nano /etc/ssh/sshd_config</pre>

Hitta raden som heter ****`PermitRootLogin Yes` och ändra den till `PermitRootLogin no`. Tryck på CTL-X och sedan Y för att spara ändringarna. För att ändringarna ska påverka måste du starta om SSH-tjänsten: 

<pre class="wp-block-preformatted">sudo service ssh restart</pre>

Om du nu avslutar den nuvarande SSH-sessionen och försöker ansluta till rootanvändaren ska du få ett felmeddelande.

Det sista steget för att säkra SSH är att inaktivera användarinloggning med ett lösenord. Detta säkerställer att angripare behöver din privata SSH-nyckel för att logga in på servern. 

Kom ihåg att om du tappar din privata nyckel kommer du att låsas från servern, så håll den säker! 

`sudo nano /etc/ssh/sshd_config`

Hitta raden som läser `PasswordAuthentication Yes` och ändra den till `PasswordAuthentication no`. Tryck på CTL-X och sedan Y för att spara ändringarna. Återigen måste du starta om SSH-tjänsten för att ändringarna ska träda i kraft. 

<pre class="wp-block-preformatted">sudo service ssh restart</pre>

Innan du loggar ut från din server bör du testa din nya konfiguration. För att göra detta öppnar du ett nytt terminalfönster utan att stänga den aktuella SSH-sessionen och försöka ansluta: 

<pre class="wp-block-preformatted">ssh kjellsson@moon.christiankjellsson.com</pre>

Du bör nu ha loggat in på servern. 

## Brandvägg

Brandväggen ger ett extra lager av säkerhet till din server genom att blockera inkommande nätverkstrafik. I den här artikeln kommer jag att visa iptables-brandväggen, som är den mest använda i Linux och som standard är installerad. För att förenkla processen att lägga till regler till brandväggen använder jag ett paket som heter ufw, som står för Okomplicerad brandvägg. Ufw-paketet installeras vanligtvis som standard, men om det inte går vidare och installerar det med följande kommando: 

<pre class="wp-block-preformatted">sudo apt-get install ufw</pre>

Nu när du har tillgång till ufw kan du börja lägga till standardreglerna, som nekar all inkommande trafik och tillåter all utgående trafik. Lägg till nu portarna för SSH (22) och HTTP (80). Om du planerar att köra en webbplats med HTTPS måste du också lägga till port 443: 

<pre class="wp-block-code"><code>sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https</code></pre>

Innan du aktiverar brandväggsreglerna, se till att porten för SSH finns i listan med tillagda regler &#8211; annars kommer du inte att kunna ansluta till din server! Standardporten är 22. Om allt ser rätt ut, gå vidare och aktivera konfigurationen: 

<pre class="wp-block-preformatted">sudo ufw enable</pre>

För att bekräfta att de nya reglerna är aktiva anger du följande kommando: 

<pre class="wp-block-preformatted">sudo ufw status verbose</pre><figure class="wp-block-image size-large">

<img src="https://christiankjellssoncom.files.wordpress.com/2019/11/image-7.png?w=877" alt="" class="wp-image-26114" srcset="https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-7.png 877w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-7-300x181.png 300w, https://www.christiankjellsson.com/wp-content/uploads/2019/11/image-7-768x464.png 768w" sizes="(max-width: 877px) 100vw, 877px" /> </figure> 

Du kommer att se att all inkommande trafik nekas som standard utom på portarna 22, 80 och 443 för både IPv4 och IPv6, vilket är en bra utgångspunkt för de flesta servrar. 

## Fail2ban

Fail2ban är ett verktyg som fungerar tillsammans med din brandvägg. Det fungerar genom att övervaka intrångsförsök mot din server och blockerar den som attackerar dig under en viss tidsperiod. Detta gör verktyget genom att lägga till alla IP-adresser som visar skadlig aktivitet i dina brandväggsregler.  
  
Fail2ban-programmet installeras inte som standard, så låt oss installera det nu: 

<pre class="wp-block-preformatted">sudo apt-get install fail2ban</pre>

Standardkonfigurationen bör räcka, vilket kommer att förbjuda en som attackerar dig i 10 minuter efter 6 misslyckade inloggningsförsök via SSH. För att säkerställa att fail2ban-tjänsten kör, ange följande kommando: 

<pre class="wp-block-preformatted">sudo service fail2ban start</pre>

Bra jobbat ! Du har nu en bra plattform för att börja bygga din WordPress webbserver och har vidtagit nödvändiga åtgärder för att förhindra obehörig åtkomst. Det är dock viktigt att komma ihåg att säkerhet är en pågående process och du bör komma ihåg följande punkter:

  * Installera endast nödvändig programvara från pålitliga källor.
  * &nbsp;Installera programvaruuppdateringar och säkerhetsfixar regelbundet.
  * &nbsp;Tvinga fram starka lösenord med ett verktyg som LastPass eller 1Password.
  * &nbsp;Använd sunt förnuft och tänk på hur du skulle få tillgång till servern om du var låst ute.

Det är allt för del 3, i nästa inlägg guidar jag dig genom installationen av Nginx, PHP-FPM och MariaDB.