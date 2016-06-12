---
layout: post
title: "Ted Xiong|Developer, Read Only Raspi"
date: 2016-06-12
---

#####Make Raspbian System Read-Only
![Alt text](/image/img.jpg)
There are many tutorials for making Raspberry pi system read only. The main purpose is protect the micro SD card from corruption. The unexpected power off or heavy write sd card cycle will corrupt the sd card. To make a respberry pi robust, make the micro sd card read only and mount another SLC SSD or HHD on it is a good solution. Yet one could certainly choose other micro computer with eMMC storage on board.

1.Install UnionFS
UnionFS is a RAM file system
<pre class="prettyprint pre-scrollable"><code>apt-get install unionfs-fuse</code></pre>