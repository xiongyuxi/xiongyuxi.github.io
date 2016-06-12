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
```powershell
apt-get install unionfs-fuse
```

2.Create mount script and make it executable
```powershell
nano /usr/local/bin/mount_unionfs

#Add the following content to this file:

#!/bin/sh
DIR=$1
ROOT_MOUNT=$(awk '$2=="/" {print substr($4,1,2)}' < /etc/fstab)
if [ $ROOT_MOUNT = "rw" ]
then
/bin/mount --bind ${DIR}_org ${DIR}
else
/bin/mount -t tmpfs ramdisk ${DIR}_rw
/usr/bin/unionfs-fuse -o cow,allow_other,suid,dev,nonempty ${DIR}_rw=RW:${DIR}_org=RO ${DIR}
fi

#Chmod this file executable

chmod +x /usr/local/bin/mount_unionfs
```

