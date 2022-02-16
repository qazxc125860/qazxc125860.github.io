### 文件管理

jdk-17_linux-aarch64_bin.tar/usr/local

-a 表示所有

pwd 查看文件路径

tar -zxvf xxx.tar.gz -C 文件路径

sz 从linux 中下载文件到windows

rz 从window 中下载文件到linux

.bat windows 下面的dos命令

,sh linux 下面的shell 脚本

1.mv 重命名

rm rm -rf强行

touch

cat

more less

tail -f 动态查询文件更新部分

<br/>

cp 文件 文件

cp -rf 文件夹 文件夹

mkdir  新建文件夹

find 路径 （./当前目录） -name(按名字查找) aa.*

whereis  -b(查询二进制文件) -m(查询说明文件) -s (源代码文件)

which (查看命令)

系统设置 date

date -s '时间'Sat Feb 12 13:48:35 CST 2022

shutdown -h now (关机)

reboot (重启)

ps -ef (查看系统的进程) = ps -aux 

kill -地址号 pid

su 切换用户

top 查看动态运载情况

uptime 查看系统负载情况

free 查看内存的使用情况

uname 查看系统信息

hostname 查看主机名

who 查看谁用过

whoami 查看当前用户名 

clear

crontab 定时任务操作

创建定时任务 crontab -e

查看任务 crontab -l

删除任务 crontab -r

\* /1 * \* \* \* echo &quot;wujinke&quot;&gt;&gt;/home/xiaowu/wujinke.log

echo 输出

\>>(重复输入不会覆盖)

\>(会覆盖)

grep  (过滤)

ps -ef |grep 查找的进程

<br/>

useradd 创建新用户

userdel 删除新用户 userdel - f tomcat 删除用户以及home 下的文件夹

password 用户名  创建或者修改

xiaz

<br/>

ifconfig

netstat -nlp 查看端口

<br/>

<br/>

#### 文件权限

文件类型  拥有者  所属用户组 其他

<br/>

\- --- --- --- -