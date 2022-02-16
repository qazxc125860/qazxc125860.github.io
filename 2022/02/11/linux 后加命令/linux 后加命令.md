### 1.配置MySQL

首先要有wget 下载命令

wget https://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm

安装

rpm -ivh mysql57-community-release-el7-8.noarch.rpm

切换

cd /etc/yum.repos.d/

安装mysql服务（绕过docker）

在yum install 版本后面加上 --nogpgcheck，即可绕过GPG验证成功安装。比如

yum install mysql-community-server --nogpgcheck

启动mysql

systemctl start mysqld

获取MySQL临时密码

grep 'temporary password' /var/log/mysqld.log

登录mysql

mysql -uroot -p

把mysql的密码校验强度改为低风险

set global validate_password_policy=LOW;

修改密码长度

set global validate_password_length=11;

修改密码

ALTER USER 'root'@'localhost' IDENTIFIED BY 'qazxc125860'; 

允许远程访问

首先关闭centos的防火墙

sudo systemctl disable firewalld

修改MySQL允许任何人连接

use mysql;

select Host,User from user;

update user set Host='%' where User ='root';

flush privileges;(刷新权限)

GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'qazxc125860' WITH GRANT OPTION;

<br/>

<br/>

TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="44ee0a32-1670-49e5-a3a2-207fb0803e71"
DEVICE="ens33"
ONBOOT="yes"

IPADDR="192.168.122.1"

GATEWAY="192.168.122.0"

NETMASK="255.255.255.0"

DNS1="144.144.144.144"

~                                                                                                           
~             