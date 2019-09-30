# linux

## 连接虚拟机centos7
[链接](https://blog.csdn.net/n950814abc/article/details/79512834)

## vi命令
[链接](https://www.cnblogs.com/sriba/p/8043471.html)
## 常用工具
    putty
    Xshell
    WinSCP
    SmarTTY
    git
## centos7安装jdk环境变量
[链接](https://www.cnblogs.com/xuliangxing/p/7066913.html)


## centos7安装 mariadb安装
[链接](https://www.cnblogs.com/zhanzhan/p/7729981.html)

```

1、安装MariaDB

安装命令

yum -y install mariadb mariadb-server
安装完成MariaDB，首先启动MariaDB

systemctl start mariadb
设置开机启动

systemctl enable mariadb
接下来进行MariaDB的相关简单配置

mysql_secure_installation
首先是设置密码，会提示先输入密码

Enter current password for root (enter for none):<–初次运行直接回车

设置密码

Set root password? [Y/n] <– 是否设置root用户密码，输入y并回车或直接回车
New password: <– 设置root用户的密码
Re-enter new password: <– 再输入一次你设置的密码

其他配置

Remove anonymous users? [Y/n] <– 是否删除匿名用户，回车

Disallow root login remotely? [Y/n] <–是否禁止root远程登录,回车,

Remove test database and access to it? [Y/n] <– 是否删除test数据库，回车

Reload privilege tables now? [Y/n] <– 是否重新加载权限表，回车

初始化MariaDB完成，接下来测试登录

mysql -uroot -ppassword
完成。


一、连接MYSQL

　　格式： mysql -h主机地址 -u用户名 -p用户密码
![20190924184408767_20962](_v_images/20190930231032220_26962.png =62x)
　　1、 连接到本机上的MYSQL。

　　首先打开DOS窗口，然后进入目录mysql\bin，再键入命令mysql -u root -p，回车后提示你输密码.注意用户名前可以有空格也可以没有空格，但是密码前必须没有空格，否则让你重新输入密码.

　　如果刚安装好MYSQL，超级用户root是没有密码的，故直接回车即可进入到MYSQL中了，MYSQL的提示符是： mysql>

　　

　　2、连接到远程主机上的MYSQL。假设远程主机的IP为：110.110.110.110，用户名为root,密码为abcd123。则键入以下命 令：

　　mysql -h110.110.110.110 -u root -p 123;(注:u与root之间可以不用加空格，其它也一样)

　　3、 退出MYSQL命令： exit (回车)


````

### MariaDB允许远程连接

> 三个设置完就可以使用了
> [链接](https://www.cnblogs.com/mapu/p/9184212.html)
> [链接](https://www.cnblogs.com/rxbook/p/8110143.html)
> [链接](https://blog.csdn.net/leejianjun/article/details/51523822)

