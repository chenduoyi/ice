# 文件权限,用户组

文件所有者 --> 创建文件的用户

文件所在组 -->与创建文件的用户同一个用户组的用户们

文件其它组 -->除开文件的所有者和其所在组的用户之外, 系统其它的用户们

查看linux所有的组
cat /etc/group --> cat 是只有查看文件, 而不能修改的命令
vi /etc/group -->vi 是可以查看, 也可以修改的命令
为了防止误操作, 对于重要的yywr, 建议使用cat 进行仅查看操作

如何在 linux 中添加组
groupadd 组名
groupadd duoduo
groupadd xiari

删除组(删除组需要组下没有用户的情况下才能成功删除)
groupdel 组名
groupdel yaoguai

创建用户, 并将用户分配到指定组
useradd -g 组名 用户名
useradd -g duoduo duoduoa
useradd -g duoduo duoduob

useradd -g xiari duoduoc

给用户设置密码
给用户设密码(如不加用户名, 默认是给当前用户自己设置密码)
passwd xiaoming 

查看所有用户信息
cat /etc/passwd
vi /etc/passwd

权限分为三种 
r    可读      4 (read)
w   可写      2 (write)
x    可执行   1 (excute)

-rw-r--r--
第一个,  代表文件的类型, - 代表普通文件, d 表示文件目录 l表示链接
rw-  --> 文件所有者的权限
r--   --> 所在组的权限
r--   -->其他组的权限

修改权限
chmod
chmod 777  --> 表示将所有者, 所有组, 其他组三者的权限均改为7, 即可读可写,可执行
当然, 也可以按需求去改, 主要是关键词是 chmod
chmod 755  --> 表示所有者, 可读, 可写, 可执行, 所有组, 与其他组可读可执行, 不可写
r     可读        4 -->2^2
w    可写        2 -->2^1
x     可执行    1 -->2^0
数值是多少, 按上面三个的权限相加就可以得出. 0 表示什么权限都没有, 4表示只读, 6表示读写, 7表示读写执行...
chmod 777 -R  目录 //-R表示递归授权

root 用户改变 其他用户所在的组, 将一个用户从一个组换到另外一个组
usermod -g 组名 用户名
usermod -g duoduo duoduoc

查看文件的所有者
ls -ahl

root修改文件的所有者
chown 用户名 文件名
chown duoduob duoduoa.txt

root 修改文件的所有组
chgrp 组名 文件名
chgrp xiari duoduoa.txt

改变用户登陆的初始目录
usermod -d 目录名 用户名





















