# Linux 文件目录操作
## 创建目录 
mkdir (make directory)
mkdir 目录名
mkdir -p 目录名/目录名  递归创建(一级一级的创建)

## 切换目录 
cd (change directory)
cd 目录名
快捷操作:
cd/cd ~ 进入当前用户的家目录
(cd 或者 cd ~ 都是快速进入当前用户家目录的命令)
cd - 进入上次目录(可以理解为, 后退一步, 到刚才所在的位置)
cd .. 进入上一级目录

## 查询当前所在目录位置
pwd (print woring directory)

## 删除目录
删除空目录(只能删除空的目录, 有内容的目录删不了)
rmdir (remove empty directories)

rm 删除文件或目录
rm (remove)
    -r 删除目录
    -f 强制删除(不再询问)
rm -rf 目录名 (强制删除目录)

## 复制文件/目录
cp 文件 目标目录 (copy)
cp file_name dir_name 指的是将文件复制到指定的目录
cp file_name dir_name/aaa 将文件复制到指定的目录, 并且改名为aaa
也就是说, 复制命令, 目录后面加了文件名, 就是复制并便命名, 如果没有加文件名, 就是原名复制过去.
    -r 复制目录
    -p 连带文件属性复制
    -d 若源文件是链接文件, 则复制链接属性
    -a 相当于 -pdr (-a 是all的意思)

## 剪切或改名命令 
mv 原文件或目录 目标目录
剪切命令与复制命令的基本一样, 不同的是, 不用加其他的-r-p一类的东西, 直接就剪切, 
如果是剪切到当前文件, 并且给了一个新的名称, 就等价于重命名的操作