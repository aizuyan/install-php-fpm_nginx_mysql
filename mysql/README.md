# install mysql by soucre code

### 准备工作
1. 安装cmake
```sh
$sudo apt-get install cmake
```
2. 安装ncurses-devel
```sh
$sudo apt-get install libncurses5-dev
```
3. 设置MYSQL用户和用户组
```sh
$groupadd mysql
$useradd -r -g mysql mysql
```
4. 创建mysql目录
```sh
$mkdir -p /usr/local/mysql
$mkdir -p /data/mysqldb
```

### 编译&安装(可能会花费很长时间)
```sh
$cmake \
> -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
> -DMYSQL_UNIX_ADDR=/usr/local/mysql/mysql.sock \
> -DDEFAULT_CHARSET=utf8 \
> -DDEFAULT_COLLATION=utf8_general_ci \
> -DWITH_INNOBASE_STORAGE_ENGINE=1 \
> -DWITH_ARCHIVE_STORAGE_ENGINE=1 \
> -DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
> -DWITH_PARTITION_STORAGE_ENGINE= 1 \
> -DSYSCONFDIR=/etc \
> -DMYSQL_DATADIR=/data/mysqldb \
> -DENABLE_DOWNLOADS=1
$
$rm CMakeCache.txt
$make
$make install
```
### 结尾工作
1. 修改mysql目录所属用户
```sh
$cd /usr/local/mysql
$chown -R mysql:mysql .
```
2. 修改mysql数据库文件目录所属用户
```sh
$cd /data/mysqldb
$chown -R mysql:mysql
```
3. 创建my.cnf文件
```sh
$cp /usr/local/mysql/support-files/my-deault.cnf /etc/my.cnf
```
编辑`/etc/my.cn`，添加下面的配置项
```sh
[mysqld]
port=3306
socket=/usr/local/mysql/mysql.sock
datadir=/data/mysqldb
character_set_server=utf8
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 
[mysql]
socket=/usr/local/mysql/mysql.sock
[mysqladmin]
socket=/usr/local/mysql/mysql.sock
```
4. 将mysql添加到服务
```sh
$sudo cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
$service mysqld status
```
如果上面可以显示MYSQL信息`* MySQL is not running`则添加服务ok
### 初始化mysql数据库
```sh
$cd /usr/local/mysql
$scripts/mysql_install_db --user=mysql --datadir=/data/mysqldb
```
执行完上面的命令，查看`/data/mysqldb`目录中的内容，如果生成了内容说明初始化成功。

### 启动MYSQL
```sh
$service mysql start
$ps aux | grep mysqld
```
如果上面的命令之后可以看到mysqld的进程说明启动mysql成功

### 修改mysql root用户密码
```sh
$cp /usr/local/mysql/bin/mysql /usr/bin/mysql
$cp /usr/local/mysql/bin/mysqladmin /usr/bin/mysqladmin
$mysqladmin -u root password '123456'
$mysql -u root -p
#输入123456密码
```
执行晚上面的命令，如果看到`Welcome to the MySQL monitor....`说明mysql安装、启动、连接ok。

### 注意事项
由于这里设置了mysql相关目录都是mysql:mysql，所以如果出现问题可以尝试sudo解决，很可能是权限的问题。
















