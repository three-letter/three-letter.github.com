---
layout: post
title: "ubuntu上安装和配置postgresql"
date: 2012-12-17 14:50
comments: true
categories: pg postgresql
---
### 1.安装postgresql

ubuntu上有现成的postgresql，故使用apt-get直接安装

	sudo apt-get install postgresql-9.1

### 2.创建用户组和用户

postgresql需要一个专门的用户才能使用

	sudo groupadd postgresql
	sudo useradd -g postgres postgresql

需要给用户postgres更改密码

	sudo passwd postgres

### 3.创建数据库文件存储目录并给postgres赋权

	sudo mkdir /usr/local/pgsql/data
	cd /usr/local/pgsql
	sudo chown -R postgres:postgresql data

### 4.初始化数据库目录

ubuntu默认安装pg目录为: /usr/lib/postgresql/9.1

	su postgres
	/usr/lib/postgresql/9.1/bin/initdb -D /usr/local/pgsql/data

### 5.启动数据库

	su postgres
	/usr/lib/postgresql/9.1/bin/postmaster -D /usr/local/pgsql/data

### 6.给postgresql命令做软连接，方便之后的操作

	sudo ln -s /usr/lib/postgresql/9.1/bin/* /usr/bin
