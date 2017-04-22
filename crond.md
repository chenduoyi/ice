文件位置
位置一般在/var/spool/cron/下，如果你是root用户，那下面有个root文件，建议日常备份，避免误删除导致crontab 文件丢失；

crontab -e
初次运行时, 会提示选择编辑器
通常选择3, vim, 这个比较常用和熟悉
(如果选了其它的, 然后要切换回来
sudo select-editor
)

自动任务设置执行时间
一共有五个参数, 依次是: 分钟, 小时, 天, 月, 星期
自动任务示例:
* * * * * date >> /home/mydate2
//每分钟, 每小时, 每天, 每月, 每一个星期数, 往/home/mydate2 文件里, 写入当前日期时间

如果需写多条自动任务, 一是可以在crontab 中 直接写入多条任务, 每条任务占一行
* * * * * date >> /home/mydate2
* * * * * cp /home/mydate2 /root

#每天的21:30 重启apache
#30 21 * * * service httpd restart

#每月1号,10号,20号 21:30 重启apache
#30 21 1,10,20 * * service httpd restart

#每月1到10号的21:30 重启apache
30 21 1-10 * * service httpd restart

小结
 * 表示任何时候都匹配
可以用1,2,3 表示几个时间点
可以用1-10 表示1到10的区间
可以用*/x , 表示每x分钟(或x小时)执行一次

动态查看文件内容
tail -f /tmp/testcrond/date.txt


第二种办法是, 把需要自动执行的各种任务, 写入一个可执行文件, 然后在自动任务中, 执行这个文件即可
以.sh结尾, 例: mytask.sh, 表示一个可执行文件.
然后在crontab 文件中, 直接写入文件路径, 表示按指定时间 , 执行一次该文件
crontab -e
* * * * *  /root/mytask.sh

注意, 修改了crontab 自动任务之后, 要重启一下, 才能生效!
一种方法是, 直接到cron 的目录下, 
/etc/init.d/crond restart

另一种方法是, 直接用service crond restart
(前提是crond要加入到service系统服务中去)

