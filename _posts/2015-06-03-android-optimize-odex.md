---
layout: page
title: "aDesk Odex优化，加速启动和反盗版"
teaser: "VDI aDesk是一个Android系统，作为搞机3年的孩子来说，不运用一点Android社区的优化知识，感觉不很爽……"
subheadline: "Odex优化"
description: ""
tags: 
    - VDI
    - aDesk
    - Android
categories:
    - AndroidOpimize
# permalink: /courses/android-optimize/
header:
    image_fullwidth: "android-robo.jpg"
---

## 什么是Odex优化
&emsp;&emsp;ODEX是安卓上的应用程序apk中提取出来的可运行文件，即将APK中的classes.dex文件通过dex优化过程将其优化生成一个·dex文件单独存放，原APK中的classes.dex文件会保留。

相关的百科: [ODEX百度百科](http://baike.baidu.com/item/ODEX){:target="brank"}

效果、优点、缺点上边都已写明了，现在只说说他的优点:

> <b>Odex化后系统启动和程序运行速度大大提高，稳定性不变。因此推荐做Odex化。</b>

> 1. <b>刷完机首次进入系统的时间会缩短一些</b>，文件的运行速度应该也有所提升。
> 2. APK文件不能单独安装，并且如果反编译APK文件，一般也只能得到资源文件。可以说是起到一定的保护作用，<mark>避免被肆意修改和使用</mark>。这样做可以使其厂商保证一定的反盗版，因为没有dex文件的apk是无法正常安装的。
> 3. 会增加一些可安装应用的空间，虽然不是很多。
> 4. 某些机身内存太小的手机优化的时候可以删除dex文件来达到制作大内存包的目的，但是这种大内存包会使手机软件启动速度变慢。适合不追求速度，需要更多内存装软件的用户。

## Odex优化开启方法

最简单最有效的就是参考开源代码啦！

在`BoardConfig.mk`或`device.mk`上添加[以下一段代码](https://github.com/CyanogenMod/android_device_intel_mixins/blob/cm-12.1/groups/art-config/default/BoardConfig.mk){:target="brank"}:

    # Enable dex-preoptimization to speed up the first boot sequence
    # Note that this operation only works on Linux for now
    # Enable for non-eng builds
    ifneq ($(TARGET_BUILD_VARIANT),eng)
    WITH_DEXPREOPT := true
    endif

&emsp;&emsp;这样子，在以`eng`模式编译时，不启用ODEX优化，方便反编译APK调试问题，在以`user`或`userdebug`模式编译源代码时，则会自动地启用ODEX优化，以达到加速启动、提升运行速度的目的。
