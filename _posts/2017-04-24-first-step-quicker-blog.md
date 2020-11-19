---
id: 25903
title: First step to a quicker blog
date: 2017-04-24T10:54:39+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=25903
permalink: /2017/04/24/first-step-quicker-blog/
amazonS3_cache:
  - 'a:9:{s:80:"//christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017.png";i:25904;s:64:"//christiankjellsson.com/wp-content/uploads/2017/04/CF-Cache.png";i:25908;s:86:"//christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017-Test2.png";i:25910;s:88:"//christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017-768x555.png";i:25904;s:72:"//christiankjellsson.com/wp-content/uploads/2017/04/CF-Cache-768x180.png";i:25908;s:94:"//christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017-Test2-768x555.png";i:25910;s:88:"//christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017-300x217.png";i:25904;s:71:"//christiankjellsson.com/wp-content/uploads/2017/04/CF-Cache-300x70.png";i:25908;s:94:"//christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017-Test2-300x217.png";i:25910;}'
categories:
  - Computer
  - For the fun of it
---
I&#8217;m going to replace the old server set-up for this Digitalocean VPS. Today the server is running on a vanilla PHP5-FPM, Nginx and MariaDB.<!--more-->

But first I want to make some test and see how much I can squeeze out of the vanilla installation om LEMP. Let try to see what Pingdom Tools gives me as an initial result.

Could it be possible to get it even lower in Load Time? Maybe use of FastCGI Cache and other Cache tools. Lets see. First step is to the fix the Preformance Insights that are rated E and F.

<img class="alignnone wp-image-25904 size-full" src="http://christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017.png" alt="" width="971" height="702" /> 

&nbsp;

## Remove query strings from static resources

> Resources with a &#8220;?&#8221; in the URL are not cached by some proxy caching servers. Remove the query string and encode the parameters into the URL for the following resources:
> 
> /wp-includes/css/somestylesheet**.min.css?ver=4.4.2**

Okay, this one is easy. Open functions.php and add this code block  
`function _remove_script_version( $src ){<br />
$parts = explode( '?ver', $src );<br />
return $parts[0];<br />
}<br />
add_filter( 'script_loader_src', '_remove_script_version', 15, 1 );<br />
add_filter( 'style_loader_src', '_remove_script_version', 15, 1 );`

## Leverage browser caching

> The following cacheable resources have a short freshness lifetime. Specify an expiration at least one week in the future for the following resources:

Oh I see. Since I use CloudFlare as a CDN, CloudFlare are doing all the cache of static content (such as .css, .js and .png) on their edge servers around the world. Super easy to fix.

Sign-in into you Cloudflare account. Find you domain and navigate to **Caching** and change the time to lets say a month.

<img class="alignnone wp-image-25908 size-full" src="http://christiankjellsson.com/wp-content/uploads/2017/04/CF-Cache.png" alt="" width="982" height="230" /> 

Okay, now what happend to the Pingdom results?

<img class="alignnone size-full wp-image-25910" src="http://christiankjellsson.com/wp-content/uploads/2017/04/pingdom-tools-24-04-2017-Test2.png" alt="" width="972" height="702" />