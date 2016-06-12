---
layout: post
title:  "Make Raspbian System Read-Only"
desc: "Make Raspbian System Read-Only"
keywords: "Raspbian,blog,read only"
date: 2015-01-08
categories: [raspberry]
tags: [blog]
icon: fa icon-raspberrypi
---

There are many tutorials for making Raspberry pi system read only. The main purpose is protect the micro SD card from corruption. Without read only file system, The Raspberry Pi will usually face micro-SD card corruption due to heavy write on card and suddenly unexpected power off.

1.Install UnionFS, UnionFS is a RAM file system
'''powershell
apt-get install unionfs-fuse
'''
