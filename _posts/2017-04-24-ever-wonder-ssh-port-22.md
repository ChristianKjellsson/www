---
id: 25896
title: Ever wonder why SSH is port 22?
date: 2017-04-24T09:53:30+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=25896
permalink: /2017/04/24/ever-wonder-ssh-port-22/
categories:
  - Computer
  - Good to know
---
Have you ever wonder why SSH daemon is listening on port 22 and not port Something-else? Wonder no more.<!--more-->

**Tatu Ylonen** published the secret behind port 22.

> Anyway, I designed SSH to replace both telnet (port 23) and ftp (port 21). Port 22 was free. It was conveniently between the ports for telnet and ftp. I figured having that port number might be one of those small things that would give some aura of credibility. But how could I get that port number? I had never allocated one, but I knew somebody who had allocated a port.

Since this was in the early days of the Internet Tatu had to ask for permission to get the port 22 so he emailed Internet pioneers **Jon Postel** and **Joyce K. Reynolds**.

`From ylo Mon Jul 10 11:45:48 +0300 1995<br />
From: Tatu Ylonen<br />
To: Internet Assigned Numbers Authority<br />
Subject: request for port number<br />
Organization: Helsinki University of Technology, Finland</p>
<p>Dear Sir,</p>
<p>I have written a program to securely log from one machine into another<br />
over an insecure network.  It provides major improvements in security<br />
and functionality over existing telnet and rlogin protocols and<br />
implementations.  In particular, it prevents IP, DNS and routing<br />
spoofing.  My plan is to distribute the software freely on the<br />
Internet and to get it into as wide use as possible.</p>
<p>I would like to get a registered privileged port number for the<br />
software.  The number should preferably be in the range 1-255 so that<br />
it can be used in the WKS field in name servers.</p>
<p>I'll enclose the draft RFC for the protocol below.  The software has<br />
been in local use for several months, and is ready for publication<br />
except for the port number.  If the port number assignment can be<br />
arranged in time, I'd like to publish the software already this week.<br />
I am currently using port number 22 in the beta test.  It would be<br />
great if this number could be used (it is currently shown as<br />
Unassigned in the lists).</p>
<p>The service name for the software is "ssh" (for Secure Shell).</p>
<p>Yours sincerely,</p>
<p>Tatu Ylonen </p>
<p>... followed by protocol specification for ssh-1.0`

Just the next Tatu Ylonen recieved and reply back.

`Date: Mon, 10 Jul 1995 15:35:33 -0700<br />
From: jkrey@ISI.EDU<br />
To: ylo@cs.hut.fi<br />
Subject: Re: request for port number<br />
Cc: iana@ISI.EDU</p>
<p>Tatu,</p>
<p>We have assigned port number 22 to ssh, with you as the point of<br />
contact.</p>
<p>Joyce`

Source: <a href="https://www.ssh.com/ssh/port" target="_blank" rel="noopener noreferrer">The story of getting SSH Port 22 </a>