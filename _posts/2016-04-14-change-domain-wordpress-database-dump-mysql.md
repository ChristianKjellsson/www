---
id: 66
title: Change Domain on WordPress Database dump in MySQL
date: 2016-04-14T16:57:13+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=66
permalink: /2016/04/14/change-domain-wordpress-database-dump-mysql/
categories:
  - Snippets
---
How to change the domain name on all post, attachments and meta values in a WordPress database, from commandline.  
<!--more-->

`/* Begin Here */<br />
UPDATE wp_posts SET guid = replace(guid, 'http://olddomain.com','http://newdomain.com');<br />
UPDATE wp_posts SET post_content = replace(post_content, 'http://olddomain.com', 'http://newdomain.com');<br />
UPDATE wp_links SET link_url = replace(link_url, 'http://olddomain.com', 'http://newdomain.com');<br />
UPDATE wp_links SET link_image = replace(link_image, 'http://olddomain.com', 'http://newdomain.com');<br />
UPDATE wp_postmeta SET meta_value = replace(meta_value, 'http://olddomain.com', 'http://newdomain.com');<br />
UPDATE wp_usermeta SET meta_value = replace(meta_value, 'http://olddomain.com', 'http://newdomain.com');<br />
/*UPDATE wp_options SET option_value = replace(option_value, 'http://olddomain.com', 'http://newdomain.com') WHERE option_name = 'home' OR option_name = 'siteurl' OR option_name = 'widget_text' OR option_name = 'dashboard_widget_options';*/<br />
UPDATE wp_options SET option_value = replace(option_value, 'http://olddomain.com', 'http://newdomain.com');`