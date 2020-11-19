---
id: 59
title: Simple rotating AWS S3 Backup Script
date: 2016-04-08T18:32:47+00:00
author: Christian Kjellsson
layout: post
guid: http://christiankjellsson.com/?p=59
permalink: /2016/04/08/amazon-aws-s3-backup-script/
categories:
  - Snippets
---
A very simple but yet effective script if you would like to backup onto Amazon S3. <!--more-->The script is explain inline but it&#8217;s going to zip a specific folder, lets say your webroot, then place the zip fil(tar.gz) in another folder /backups and then upload the files to your Amazon AWS account. If a file in /backup is folder than 7 days it gets delete, both on your Amazon account and in /backup, hence the rotating part.

## Start with AWS CLI

Install <a href="http://docs.aws.amazon.com/cli/latest/userguide/installing.html" target="_blank" rel="noopener noreferrer">Amazon Commandline tools</a>  
nano script.sh

## Bash script 

`#!bin/sh<br />
SERVER=$(hostname)<br />
#where is your webroot?<br />
WWW="/var/www"<br />
#Target backup-folder<br />
S3DUMP="/backups/"<br />
# AWS S3 Bucket name.<br />
S3BUCKET="YOURBUCKETNAME_AT_AMAZON"<br />
# Tar the folder with current hostname and date.<br />
tar -zvcf $S3DUMP/$(date +%Y-%m-%d_kl%H)_$SERVER.tar.gz $WWW<br />
# Any files older than 7 days? If yes, delete.<br />
find $S3DUMP/* -mtime +7 -exec rm {} ;<br />
# Upload to AWS S3.<br />
/usr/local/bin/aws s3 sync $S3DUMP s3://$S3BUCKET --delete`