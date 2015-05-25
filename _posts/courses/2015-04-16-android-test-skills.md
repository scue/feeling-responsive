---
layout: page-fullwidth
title: "Andriod常用工具"
description: ""
tags: 
    - Android
    - Tools
categories:
    - courses
permalink: /courses/android-test-skills/
header:
    image_fullwidth: "unsplash_brooklyn-bridge_header.jpg"
image:
    thumb: "unsplash_brooklyn-bridge_thumb.jpg"
---
<div class="row">
<div class="medium-4 medium-push-8 columns" markdown="1">
<div class="panel radius" markdown="1">
**Table of Contents**
{: #toc }
*  TOC
{:toc}
</div>
</div><!-- /.medium-4.columns -->



<div class="medium-8 medium-pull-4 columns" markdown="1">

# 常用工具

主题：主要讲解一些常用的一些命令行，及定位问题的方法

### 1.  抓图：screencap

	screencap -p /sdcard/Pictures/ScreenShot_$(date +%F_%H-%M-%S).png

### 2.  Kernel版本信息

	cat /proc/version

### 3.  Kernel接收传入参数
    
	cat /proc/cmdline

### 4.  清空并抓取Logcat日志

	adb logcat -c && adb logcat -v threadtime

### 5.  Logcat详细信息

	adb logcat -v threadtime

### 6.  Top

	adb shell
	while busybox true; do top -m 10 -d 3 -t -n 1 | busybox \
	    awk '{now=strftime("%Y-%M-%d %T "); print now $0}'; done

### 7.  Vmstat

	adb shell vmstat -d 3 | busybox \
	    awk '{now=strftime("%Y-%M-%d %T "); print now $0}'

### 8.  网络分析

	adb shell netcfg
	# or
	adb busybox ifconfig -a
	
### 9.  查看进程

	ps -P
	ps -t -p -P # with thread

| 参数 | 含义 |
|--------|--------|
|USER  | 进程的当前用户；|
|PID   | process ID的缩写，也就进程号；|
|PPID  | process parent ID，父进程ID|
|VSIZE | virtual size，进程虚拟地址空间大小；|
|RSS   | 进程正在使用的物理内存的大小；|
|WCHAN | 进程如果处于休眠状态的话，在内核中的地址；|
|PC    | program counter，|
|NAME  | process name，进程的名称|
|NICE  | 进程优先级|
|SCHED | 进程调度|

### 10.	查看存储空间

	df
	busybox df

### 11.	查看数据库

	sqlite3 /path/to/xx.db

### 12.	查看内存信息

	cat /proc/meminfo
	busybox free
	vmstat

### 13.	分辨率信息

	find /sys -iname “*vga*”
	/sys/devices/platform/rk30_i2c.2/i2c-2/2-0050/display/display0.VGA/mode \
	    # 通过上一行获得

### 14.	查看、设置属性信息

	getprop
	setprop

### 15. 检查流量

	iftop

### 16. showmap

`showmap`用来检查一个进程，它调用了哪些动态库

    showmap -t $(busybox pidof surfaceflinger)
