# install nginx by source code

### 安装步骤
#### 解压源码包
```shell
$tar -zxvf nginx-1.8.0.tar.gz
$tar -zxvf pcre-8.36.tar.gz
$tar -zxvf zlib-1.2.8.tar.gz
```
#### 安装依赖包
```sh
$sudo apt-get install openssl openssl-devel
```
#### 编译选项
```shell
./configure \
--prefix=/usr/local \
--sbin-path=/usr/local/nginx/nginx \
--conf-path=/usr/local/nginx/nginx.conf \
--pid-path=/usr/local/nginx/nginx.pid \
--with-http_ssl_module \
--with-pcre=../pcre-8.36 \
--with-zlib=../zlib-1.2.8
$make
$make install
```

### 启动nginx
```sh
$/usr/local/nginx/nginx
#几个常用的nging命令
$/usr/local/nginx -t    #测试默认为值的配置文件是否ok
$/usr/local/nginx -c /etc/nginx.conf #指定nginx解析的配置文件
$/usr/local/nginx -s stop|quit|reload|reopen  #停止或者重启nginx
```

### 效果
在浏览器中输入localhost，如果看到Welcome to Nginx!则说明安装nginx成功。

### 常见问题
#### 编译调试模块——echo
```sh
$git clone https://github.com/openresty/echo-nginx-module
$./configure \
--prefix=/usr/local \
--sbin-path=/usr/local/nginx/nginx \
--conf-path=/usr/local/nginx/nginx.conf \
--pid-path=/usr/local/nginx/nginx.pid \
--with-http_ssl_module \
--with-pcre=../pcre-8.36 \
--with-zlib=../zlib-1.2.8 \
--add-module=../echo-nginx-module
```
