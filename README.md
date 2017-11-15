# hello-word

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



