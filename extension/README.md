# part php extension install

## imagick
[imageMagick源码包](http://pan.baidu.com/s/1sjMiwk1)，密码：1rmz
[php imagick源码包](http://pan.baidu.com/s/1eQdP1ZG)，密码：fbir
编译安装
```sh
$tar -zxvf ImageMagick.tar.gz
$cd ImageMagick-6.9.2-5
$./configure --prefix=/usr/local/imagemaick
$make 
$make install
$tar -xvf imagick-3.0.1.tgz
$cd imagick-3.0.1
$ /usr/local/php/bin/phpize
$./configure
$./configure --with-php-config=/usr/local/php/bin/php-config --with-imagick=/usr/local/imagemagick
$make
$make install
```
完成之后在php.ini中添加`extension="imagick.so"`

## memcache

编译安装
```sh
$tar -zxvf memcached-1.4.24.tar.gz
$cd memcached-1.4.24
$./configure --prefix=/usr/local/memcached
$make 
$make install
$tar -xvf memcache-2.2.7.tgz
$cd memcache-2.2.7
$ /usr/local/php/bin/phpize
$./configure
$ ./configure --with-php-config=/usr/local/php/bin/php-config --enable-memcache --with-zlib-dir
$make
$make install
```
完成之后在php.ini中添加`extension="memcache.so"`

## redis
[redis扩展源码包](http://pan.baidu.com/s/14vSVO)，密码：dvxe
```sh
$tar -zxvf phpredis-2.2.4.tar.gz
$cd phpredis-2.2.4
$/usr/local/php/bin/phpize
$ ./configure --with-php-config=/usr/local/php/bin/php-config
$make && make install
```
完成之后在php.ini中添加`extension="redis.so"`

## seaslog
[seaslog扩展源码包](http://pan.baidu.com/s/1kTD7gxD)，密码：qnx9
安装和redis基本一致

## phalcon