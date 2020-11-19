---
id: 61
title: Nginx, FastCGI Cache with PHP5
date: 2016-04-08T18:36:20+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=61
permalink: /2016/04/08/nginx-fastcgi-cache-php5/
categories:
  - Snippets
---
Server Block for Nginx setup with PHP5 and FastCGI Cache that write HTML files to RAM-Memory. Old Guide &#8211; Use with caution since PHP7 is a standard in 2017.  
<!--more-->

`server {<br />
    listen 80;<br />
    server_name domain.com www.domain.com;<br />
    return 301 https://www.domain.com$request_uri;<br />
}<br />
server {<br />
	listen 443 ssl;<br />
	server_name domain.com www.domain.com;</p>
<p>	ssl_certificate /etc/nginx/ssl/domain.crt;<br />
	ssl_certificate_key /etc/nginx/ssl/domain.key;</p>
<p>	root /srv/www/domaincom;<br />
        index index.php index.html index.htm;</p>
<p>        location / {<br />
		#try_files $uri $uri/ /index.php?$args;<br />
		try_files $uri $uri/ /index.php$is_args$args;</p>
<p>        }</p>
<p>        # pass the PHP scripts to FastCGI server listening on /var/run/php5-fpm.sock<br />
        location ~ .php$ {<br />
                try_files $uri =404;<br />
                fastcgi_pass unix:/var/run/php5-fpm.sock;<br />
                fastcgi_index index.php;<br />
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;<br />
                include fastcgi_params;</p>
<p>		fastcgi_cache_bypass $skip_cache;<br />
	        fastcgi_no_cache $skip_cache;</p>
<p>		fastcgi_cache WORDPRESS;<br />
		fastcgi_cache_valid  60m;<br />
        }</p>
<p>	set $skip_cache 0;<br />
	location ~ /purge(/.*) {<br />
	    fastcgi_cache_purge WORDPRESS "$scheme$request_method$host$1";<br />
	}</p>
<p>	if ( $arg_add-to-cart != "" ) {<br />
	      set $skip_cache 1;<br />
	}</p>
<p>	if ($request_uri ~* "/store.*|/cart.*|/my-account.*|/checkout.*|/addons.*|/wishlist.*") {<br />
         set $skip_cache 1;<br />
	}</p>
<p>	# POST requests and urls with a query string should always go to PHP<br />
	if ($request_method = POST) {<br />
		set $skip_cache 1;<br />
	}<br />
	if ($query_string != "") {<br />
		set $skip_cache 1;<br />
	}</p>
<p>	# Don't cache uris containing the following segments<br />
	if ($request_uri ~* "/wp-admin/|/xmlrpc.php|wp-.*.php|/feed/|index.php|sitemap(_index)?.xml") {<br />
		set $skip_cache 1;<br />
	}</p>
<p>	# Don't use the cache for logged in users or recent commenters<br />
	if ($http_cookie ~* "comment_author|wordpress_[a-f0-9]+|wp-postpass|wordpress_no_cache|wordpress_logged_in") {<br />
		set $skip_cache 1;<br />
	}</p>
<p>}`