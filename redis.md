# redis 安装与自动启动

## redis安装

下载文件到 /usr/local/src 目录下

```wget http://download.redis.io/releases/redis-2.8.13.tar.gz```

解压文件

tar zxvf redis-2.8.13.tar.gz

切换目录到 redis-2.8.13 目录下

cd redis-2.8.13

执行make命令

make

现在就可以启动redis了，redis只有一个启动参数，就是他的配置文件路径。

```redis-server /etc/redis.conf```

注意，默认复制过去的redis.conf文件的daemonize参数为no，所以redis不会在后台运行，这时要测试，我们需要重新开一个终端。修改为yes则为后台运行redis。另外配置文件中规定了pid文件，log文件和数据文件的地址，如果有需要先修改，默认log信息定向到stdout.

下面是redis.conf的主要配置参数的意义：

- daemonize：是否以后台daemon方式运行
- pidfile：pid文件位置
- port：监听的端口号
- timeout：请求超时时间
- loglevel：log信息级别
- logfile：log文件位置
- databases：开启数据库的数量
- save \* \*：保存快照的频率，第一个*表示多长时间，第三个\*表示执行多少次写操作。在一定时间内执行一定数量的写操作时，自动保存快照。可设置多个条件。
- rdbcompression：是否使用压缩
- dbfilename：数据快照文件名（只是文件名，不包括目录）
- dir：数据快照的保存目录（这个是目录）
- appendonly：是否开启appendonlylog，开启的话每次写操作会记一条log，这会提高数据抗风险能力，但影响效率。
- appendfsync：appendonlylog如何同步到磁盘（三个选项，分别是每次写都强制调用fsync、每秒启用一次fsync、不调用fsync等待系统自己同步）

这时你可以打开一个终端进行测试了，配置文件中默认的监听端口是6379

我们可以开启一个Redis客户端进行测试
```
[root@SNDA-192-168-1-114 ~]# redis-cli 
Could not connect to Redis at 127.0.0.1:6379: Connection refused 
not connected> exit 
[root@SNDA-192-168-1-114 ~]# redis-server /etc/redis.conf 
[root@SNDA-192-168-1-114 ~]# redis-cli 
redis 127.0.0.1:6379> quit
```
## phpredis扩展
下载文件到 /usr/local/src 目录下：

```wget https://github.com/nicolasff/phpredis/archive/2.2.4.tar.gz```
解压文件

tar zxvf phpredis-2.2.4.tar.gz

进入安装目录

cd phpredis-2.2.4

用phpize生成configure配置文件 

/usr/local/php/bin/phpize

phpize就是用来生成php扩展包的安装配置文件, configure, 有些文章直接说, 执行 phpize, 却没说, 这个phpize需要写上具体的路径
./configure --with-php-config=/usr/local/php/bin/php-config  #配置 注意, 指定php config路径时, 这里的'=', 等号左右两边不能加空格, 加了空格就会报错.

make  #编译

make install  #安装

安装完成之后，出现下面的安装路径

/usr/local/php/lib/php/extensions/no-debug-non-zts-20090626/

配置php支持

vi /usr/local/php/etc/php.ini

#编辑配置文件，在最后一行添加以下内容

extension="redis.so"

#注意, 单词不要写错

wq

#保存退出

## 重启服务

重启nginx && php-fpm 两个都重启, 才能生效.
