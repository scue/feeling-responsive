---
layout: page-fullwidth
title: "Linux MySql使用笔记"
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

### 1. 安装MySql

```
sudo apt-get install mysql-server mysql-client
```

### 2. 增加用户

新建用户`ssl-emm`，授权任意地址`%`允许访问，密码为`password`

    mysql -u root --password=passwd
    >use mysql; 
    >GRANT ALL PRIVILEGES ON emm_base.* TO 'ssl-emm'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION; 
    >FLUSH PRIVILEGES;
    >quit

### 3. 查看数据库

    mysql -h localhost -u root -ppassword
    >show databases;
    >use bedrock; /*使用 bedrock 数据库*/
    >create table employee (Name char(20),Dept char(20),jobTitle char(20));
    >DESCRIBE employee; /*相当于 show dolumns from employee; */
    >show tables; /*显示数据表*/
    >INSERT INTO employee VALUES ('Fred Flinstone','Quarry Worker','Rock Digger');
    >INSERT INTO employee VALUES ('Wilma Flinstone','Finance','Analyst');
    >INSERT into employee values ('Barney Rubble','Sales','Neighbor');
    >INSERT INTO employee VALUES ('Betty Rubble','IT','Neighbor');
    >quit

### 4. 数据表操作

选择(select)、插入(insert)、删除(delete)

    mysql -uemm -pemm
    >use emm_base;
    >select * from tb_gwid_white_list;
    >insert into tb_gwid_white_list(gwid, note) values('C44F48D1', '20141202 lwq - 200.200.139.93 add');
    >delete from tb_gwid_white_list where id = 12;
    >quit

### 5. Root对外开放

    mysql -uroot -ppassword
    >select host,user from user; /*查看用户的权限情况*/
    >select host, user, password from user;
    >Grant all privileges on *.* to 'root'@'%' identified by 'password' with grant option; /*允许所有地址'%'使用root来访问数据库*/
    >select host, user, password from user;
    >quit

### 6. Root密码遗忘

*   更新密码

        sudo service mysql stop
        sudo mysqld --skip-grant-tables &
        sudo mysql -u root mysql
        >UPDATE user SET Password=PASSWORD('my_password') where USER='root';
        >FLUSH PRIVILEGES;
        >quit
        sudo pkill mysql

*   重启服务

        sudo service mysql restart

*   验证密码

        mysql -u root -p #输入'my_password'

### ~. 相关链接

1. [MySQL on Linux Tutorial](http://www.yolinux.com/TUTORIALS/LinuxTutorialMySQL.html)
