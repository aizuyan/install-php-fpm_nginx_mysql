# install php by source code

### 准备工作
1. freetype安装——生成验证码可能会用到
```sh
$tar -xvf freetype-2.4.0.tar.bz2
$cd freetype-2.4.0
$./configure --prefix=/usr/local/freetype
$make
$make install
```
2. 安装curl、png、mcrypt
```sh
apt-get install curl libcurl3 libcurl3-dev
$apt-get install libpng3 libpng3-dev
$apt-get install libmcrypt4 libmcrypt-dev
```

### 编译安装
```sh
./configure \
--prefix=/usr/local/php \
--with-config-file-path=/usr/local/php/etc \
--enable-fpm \
--enable-pcntl \
--enable-mysqlnd \
--enable-opcache \
--enable-sockets \
--enable-sysvmsg \
--enable-sysvsem  \
--enable-sysvshm \
--enable-shmop \
--enable-zip \
--enable-ftp \
--enable-soap \
--enable-xml \
--enable-mbstring \
--with-mysql=/usr/local/mysql 
--with-pdo-mysql=/usr/local/mysql \
--with-pcre-regex \
--with-iconv \
--with-zlib \
--with-mcrypt \
--with-gd \
--with-openssl \
--with-mhash \
--with-xmlrpc \
--with-curl \
--with-imap-ssl \
--enable-pdo \
--with-freetype-dir=/usr/local/freetype
$
$make
$make install
```
### php配置
1. php.ini管理
看看`/usr/local/php/etc`下面是否又配置文件，有的话cp一份命名为php.ini，没有的话将源码包里面的php.ini*复制一份过来命名为php.ini
2. php-fpm.conf管理
php-fpm.conf一般在安装目录的/usr/local/php/etc/php-fpm.conf.default这个位置
```sh
$cd /usr/local/php/etc
$cp php-fpm.conf.default php-fpm.conf
```
修改php-fpm.conf中的内容，主要是绑定的ip、端口或者unix socket，下面是我的配置，可以适当参考
```sh
pid = run/php-fpm.pid
error_log = log/php-fpm.log
log_level = notice
daemonize = yes
rlimit_files = 1024
user = nobody
group = nobody
listen = 127.0.0.1:9000
pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
```
### 启动php-fpm
```sh
$cp /usr/local/php/sbin/php-fpm /usr/bin/php-fpm
$php-fpm -t     #测试默认配置文件是否ok
$php-fpm
$ps aux | grep php-fpm
```
如果看到php-fpm的进程说明php-fpm启动成功。
php-fpm的结束
```sh  
$kill -INT `cat /usr/local/php/var/run/php-fpm.pid`
```

