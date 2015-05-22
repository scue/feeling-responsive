---
layout: page-fullwidth
title: "Linux命令行技巧"
header: no
categories:
    - courses
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

## 一、项目相关

+   EMM测试小技巧: [emm_test_tips](http://200.200.0.36/28120/emm_test_tips)
+   VDI测试小技巧: [vdi_test_tips](http://200.200.0.36/28120/vdi_test_tips)

## 二、常用命令行

### 1. 复制显示进度条

    # 语法:
    rsync -avub -e ssh  --progress SRC... DEST
    # 举例:
    rsync -avub -e ssh  --progress root@200.200.139.79:/tmp/lee .
    # 作用: 将在本地创建 lee 目录，并完全复制远程机器的/tmp/lee内容

### 2. 挂载远程目录至本地(ssh)

    # 语法:
    sshfs [user@]host:[dir] mountpoint [options]
    # 举例:
    sshfs -o follow_symlinks -p 2222 root@192.168.1.194:/ /media/scue/nexus4root
    # 作用: 把一台手机设备根目录/挂载到本地目录下

### 3. 挂载远程目录到本地(nfs)

server:

-   安装软件: `sudo apt-get install nfs-kernel-server`

-   编辑配置: `sudo vi /etc/exports`

        /home 200.200.137.171(rwync,no_root_squash)
        /media/Source 200.200.137.171(rwync,no_root_squash)

-   启动服务: `sudo service nfs-kernel-server start`

client:

-   安装软件: `sudo apt-get install nfs-common`

-   挂载目录: `sudo mount 200.200.137.175:/media/Source /media/sinfor/lwq175`