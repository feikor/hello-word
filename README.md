# subversion

查询是否安装  
rpm -qa subversion
如果没有使用
yum -y install  subversion

配置svn并启动svn服务,可以使用svnserve --help查看启动帮助,其中箭头指出来的配置项比较常用
指定svn的数据存储路径
mkdir -p /virtualhost/svn

#指定svn的配置文件信息路径
#mkdir -p /virtualhost/svn/svnpasswd

启动svn服务
svnserve -d -r /virtualhost/svn/


检测svn服务是否正常启动,如果能看到下图所示则证明启动成功
第一通过进程检测
ps -ef | grep svn
第二通过端口3690检测
netstat -lntup | grep 3690
第三通过文件检测,需要root用户才可以执行
lsof -i :3690

使用svnadmin建立svn项目版本库
查看创建项目版本库命令
svnadmin --help
svnadmin help create
创建sadoc版本库
 svnadmin create /virtualhost/svn/www.bibomb.com
 
 
 配置sadoc版本可的权限
     进入sadoc版本库配置目录,并备份配置文件
    cd /application/svndata/sadoc/conf/
    cp -p svnserve.conf svnserve.conf.default

  进行详细配置
     anon-access = none //禁止匿名访问
     auth-access = write //认证后有读的权限
     password-db = /application/svnpasswd/passwd //指定密码文件
     authz-db = /appplication/svnpasswd/authz //指定权限认证文件


编辑passwd文件配置用户和密码
      vi passwd 
      xingmaogou = xingmaogou
      xingyuan  = xingyuan

重新启动svn服务进行验证
      杀死svn服务
       pkill svnserve
       启动svn
       svnserve -d -r /virtualhost/svn/
       备注:修改passwd和authz文件不需要重启svn服务而修改svnserve.conf则需要

#!/bin/sh


REPOS="$1"
REV="$2"

#mailer.py commit "$REPOS" "$REV" /path/to/mailer.conf
export LANG=en_US.UTF-8

CURDATE=`date`
echo "Code Deployed By at $CURDATE" >> /var/log/svn_order.log
cd /virtualhost/www/order.ip1840.com && /usr/bin/svn update --no-auth-cache --username ych --password 828282 2>>/var/log/svn_order.log

svn checkout svn://106.15.88.10/www.bibomb.com

svn checkout svn://127.0.0.1/sv.bibomb.com
svn checkout svn://localhost/sv.bibomb.com

svn co svn://203.88.211.16/sv.ip888.com --username dd  --password 33


5.@设置帐号密码

vi passwd
在[users]块中添加用户和密码，格式：帐号=密码，如dan=dan
6.@设置权限

vi authz
在末尾添加如下代码：
[/]
dan=rw
w=r
意思是版本库的根目录dan对其有读写权限，w只有读权限。

#adduser feikor
//添加一个名为tommy的用户
#passwd feikor   //修改密码4628
#usermod -g root feikor


svn://203.88.211.18/service.ip1840.com
svn://172.19.129.188/service.ip1840.com
svn://127.0.0.1/www.bibomb.com

注意事项：
post-commit文件的权限
第一次要网站目录下checkout出来
update --no-auth-cache  脚本里面忽略用户密码
 
 





