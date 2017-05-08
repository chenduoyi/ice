# redis 加入开机启动
## 开机启动脚本
```
#!/bin/sh
# chkconfig: 2345 10 90
# description: Start and Stop redis
 
PATH=/usr/local/bin:/sbin:/usr/bin:/bin
#PATH是启动脚本使用的shell的搜索路径

REDISPORT=6379
#REDISPORT指redis端口

EXEC=/opt/redis-2.8.9/src/redis-server
#redis-server的绝对路径

REDIS_CLI=/opt/redis-2.8.9/src/redis-cli
#redis-cli的绝对路径
 
PIDFILE=/var/run/redis.pid
#redis.conf配置文件中指定的pid路径地址
#在 redis.conf配置文件中需要将 daemonize 这个参数项设置为yes 才会在redis启动时生成pid文件

CONF="/etc/redis.conf"
#redis配置文件绝对路径

AUTH="1234"
#如果redis设置了登录密码，就需要这个配置
 
case "$1" in
  start)
    if [ -f $PIDFILE ]
    then
      echo "$PIDFILE exists, process is already running or crashed."
    else
      echo "Starting Redis server..."
      $EXEC $CONF
    fi
    if [ "$?"="0" ]
    then
      echo "Redis is running..."
    fi
    ;;
  stop)
    if [ ! -f $PIDFILE ]
    then
      echo "$PIDFILE exists, process is not running."
    else
      PID=$(cat $PIDFILE)
      echo "Stopping..."
      $REDIS_CLI -p $REDISPORT -a $AUTH  SHUTDOWN
      sleep 2
      while [ -x $PIDFILE ]
      do
        echo "Waiting for Redis to shutdown..."
        sleep 1
      done
      echo "Redis stopped"
    fi
    ;;
  restart|force-reload)
    ${0} stop
    ${0} start
    ;;
  *)
    echo "Usage: /etc/init.d/redis {start|stop|restart|force-reload}" >&2
    exit 1
esac
```

## 加入自启动
```
chkconfig redisd on
```