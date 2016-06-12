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

1.Install UnionFS, UnionFS is a RAM file system.

```
apt-get install unionfs-fuse
```

2.Create mount script and make it executable.

```
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

Update /etc/fstab:

```
nano /etc/fstab
```

Modify the file to read as follows:

```
proc            /proc           proc    defaults          0       0
/dev/mmcblk0p1  /boot           vfat    ro                0       2
/dev/mmcblk0p2  /               ext4    ro,noatime        0       1
mount_unionfs   /etc            fuse    defaults          0       0
mount_unionfs   /var            fuse    defaults          0       0
none            /tmp            tmpfs   defaults          0       0
```

Prepare the directories

```
cp -al /etc /etc_org
mv /var /var_org
mkdir /etc_rw
mkdir /var /var_rw
reboot
```

Done!

But, How to get raspi back to read-write for updating/upgrading/etc?

```
mount -o remount,rw /
```
