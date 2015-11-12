title: CentOS linux安装MongoDB
date: 2015-11-13
tags: MongoDB
---

### CentOS linux安装MongoDB

#### 1.安装环境
- CentOS 7 64bit（适合CentOS 5/6/7）
- mongoDB 3.0.7

#### 2.安装包（packages）
MongoDB 官方仓库里提供了一些安装包。包含以下部分：
- mongodb-org
	这是元安装包，安装这个包会自动安装以下四个组件包。

- mongodb-org-server
	这个包包含了mongod的后台进程和相关的配置信息、以及初始脚本。

- mongodb-org-mongos
	这个包包含了mongos的后台进程。

- mongod-org-shell
	这个包包含了mongo shell。

- mongodb-org-tools
	这个包包含了以下MongoDB工具：[mongoimport](https://docs.mongodb.org/manual/reference/program/mongoimport/#bin.mongoimport) ,[bsondump](https://docs.mongodb.org/manual/reference/program/bsondump/#bin.bsondump), [mongodump](https://docs.mongodb.org/manual/reference/program/mongodump/#bin.mongodump), [mongoexport](https://docs.mongodb.org/manual/reference/program/mongoexport/#bin.mongoexport), [mongofiles](https://docs.mongodb.org/manual/reference/program/mongofiles/#bin.mongofiles), [mongooplog](https://docs.mongodb.org/manual/reference/program/mongooplog/#bin.mongooplog), [mongoperf](https://docs.mongodb.org/manual/reference/program/mongoperf/#bin.mongoperf), [mongorestore](https://docs.mongodb.org/manual/reference/program/mongorestore/#bin.mongorestore), [mongostat](https://docs.mongodb.org/manual/reference/program/mongostat/#bin.mongostat),  [mongotop](https://docs.mongodb.org/manual/reference/program/mongotop/#bin.mongotop)。

#### 3.初始脚本（Init Script）
mongodb-org包里面包括了各种各样的初始脚本，其中包括`/etc/rc.d/init.d/mongod` 。这些脚本被用来`stop`，`start`，`restart`后台进程。

利用`/etc/mongod.conf`文件，并结合初始脚本，可以配置MongoDB的一些信息。
	
#### 4.注意事项
- 安装向导只支持64bit系统；
- 在`/etc/mongod.conf`文件中默认配置了只允许本地ip访问（127.0.0.1），如果你希望远程访问，请修改mongod.conf文件，将`bind_ip`那行注释掉。

#### 5.安装MongoDB
1. 配置安装包管理器（yum）
创建文件`/etc/yum.repos.d/mongodb-org-3.0.repo`，这样你可以利用`yum`命名来安装MongonDB了。

> [mongodb-org-3.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.0/x86_64/
gpgcheck=0
 enabled=1

2. 安装MongoDB包和相关工具
	当你安装包时，可以选择安装目前的版本或者之前的版本。
	安装最新的稳定版的MongoDB，执行以下命令：
	
    ```shell
    sudo yum  install -y mongodb-org
    ```

	如果要安装特定的特定的版本，命令如下

	```shell
    sudo yum install -y mongodb-org-3.0.7 mongodb-org-server-3.0.7 mongodb-org-shell-3.0.7 mongodb-org-mongos-3.0.7 mongodb-org-tools-3.0.7
    ```

#### 6.运行MongoDB
1. 启动MongoDB
	
	```shell
	sudo service mongod start
	```
	
2. 验证是否启动成功
	查看mogod是否启动成功，可以检查log文件`/var/log/mongodb/mongod.log`否有以下记录
	
	> [initandlisten] waiting for connections on port [port]

	[port]就是MongoDB对应的端口
	
3. 停止MongoDB

	```shell
	sudo service mongod stop
	```

4. 重启MongoDB

	```shell
	sudo service mongod restart
	```
#### 7.卸载MongoDB
1. 停止MongoDB

	```shell
	sudo service mongod stop
	```
	
2. 移除包
	
	```shell
	sudo yum erase $(rpm -qa | grep mongodb-org)
	```
3. 移除数据库目录
	
	```shell
	sudo rm -r /var/log/mongodb
	sudo rm -r /var/lib/mongo
	```



