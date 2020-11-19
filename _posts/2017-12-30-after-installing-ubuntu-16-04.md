---
id: 25975
title: After installing Ubuntu 16.04
date: 2017-12-30T19:22:10+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=25975
permalink: /2017/12/30/after-installing-ubuntu-16-04/
amazonS3_cache:
  - 'a:1:{s:2:"//";a:1:{s:9:"timestamp";i:1514665459;}}'
categories:
  - Computer
  - Snippets
tags:
  - Ubuntu
---
Yet another tutorial on what to do when you have installed Ubuntu 16.04. As always, these are my own notes and are written to me as a reminder.  
<!--more-->

Update the system to the latest software.  
`sudo apt update && sudo apt upgrade -y`

Install Ubuntu Restricted Extra for media codecs and Flash support.  
`sudo apt-get install ubuntu-restricted-extras`

Mediaplayer of the Mediaplayer.  
`sudo apt install vlc`

Install Spotify.  
`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys BBEBDCB318AD50EC6865090613B00F1FD2C19886`  
`echo deb http://repository.spotify.com stable non-free | sudo tee /etc/apt/sources.list.d/spotify.list`  
`sudo apt-get update && sudo apt-get install spotify-client`

Unity Tweak Tool  
`sudo apt install unity-tweak-tool`

Improve battery life and reduce overheating with TLP.  
`sudo apt install tlp tlp-rdw`  
`sudo tlp start`

Indicator Apple To Check Internet Speed.  
`sudo apt-add-repository ppa:fixnix/netspeed`  
`sudo apt update`  
`sudo apt install indicator-netspeed-unity`

Indicator Applet To Monitor System  
`sudo apt install indicator-multiload`

Install Slack.  
https://slack.com/downloads/linux

Install Skype  
https://www.skype.com/sv/get-skype/

Install LastPass.  
https://www.lastpass.com/

Install FileZilla  
`sudo apt install filezilla`

VPN  
https://www.seedboxes.cc/download/vpn/ubuntux64

Credit goes to https://itsfoss.com/