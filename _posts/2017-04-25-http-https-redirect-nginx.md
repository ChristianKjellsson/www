---
id: 25916
title: HTTP to HTTPS redirect (NGINX)
date: 2017-04-25T13:26:04+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=25916
permalink: /2017/04/25/http-https-redirect-nginx/
categories:
  - Computer
  - Snippets
---
How to redirect all traffic from http:// to https:// with Nginx server-block.<!--more-->

`server {<br />
    listen      80;   #listen for all the HTTP requests<br />
    server_name example.com www.example.com;<br />
    return      301         https://www.example.com$request_uri;<br />
}`

`server {<br />
    listen      443;   #listen for all the HTTP requests<br />
    server_name example.com www.example.com;</p>
<p>[..] rest of your Nginx Block.<br />
}`