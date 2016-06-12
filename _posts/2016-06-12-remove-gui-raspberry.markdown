---
layout: post
title:  "Remove GUI from Raspberry Pi"
desc: "Remove GUI from Raspberry Pi"
keywords: "Raspbian,GUI, remove gui"
date: 2016-06-12
categories: [raspberry]
tags: [blog]
icon: fa icon-raspberrypi
---

In some case, one does not need a GUI on raspberry pi. The advantage for removing GUI is free plenty of RAM for Raspberry Pi since its only have 1GB RAM. The following content is from internet, most of which from Stackoverflow. Please point out if there is any issue.

1.uninstall xfce4, the main GUI, the other package will remove later using autoremove


```
sudo apt-get purge xfconf xfce4-utils xfwm4 xfce4-session thunar
```

2.remove lightdm, the GUI login.
```
sudo apt-get remove lightdm
```

3.use autoremove to clean up everything
```
sudo apt-get autoremove
```

