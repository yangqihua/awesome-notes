# awesome-notes
this is some awesome notes including lots of links in the internet to setup many development environment


<h4>1.Linux服务器相关环境搭建</h4>
1.开启8080防火墙端口:  A RH-Firewall-1-INPUT -p tcp -m state -m tcp --dport 8080 --state NEW -j ACCEPT  

2.查看防火墙状态:   /etc/init.d/iptables status  
3.编辑防火墙:   vi /etc/sysconfig/iptables   
4.查看端口启动状态:   netstat -nat                 

5.添加环境变量:vi /etc/profile     
6.使环境变量生效:source /etc/profile 

7.查看系统版本:cat /etc/centos-release 

8.重启Apache: service httpd restart 



9.关闭tomcat服务器: /usr/local/tomcat/bin/shutdown.sh 

10.开启tomcat服务器:/usr/local/tomcat/bin/startup.sh 

11.配置tomcat的项目路由:<Context path="/mayi" docBase="${catalina.home}/webapps/mayi/WebRoot" reloadable="true"/> 

12.lamp安装教程：http://blog.csdn.net/xiaokuang513204/article/details/8517562

13.Jdk安装：http://www.cnblogs.com/zhoulf/archive/2013/02/04/2891608.html

14.tomcat安装：http://www.cnblogs.com/zhoulf/archive/2013/02/04/2891633.html

<h4>2.mysql安装卸载，配置相关</h4>

1.mysql重启: /etc/init.d/mysqld restart  
2.卸载mysql:<br>
(1).yum remove mysql*
(2)、查找以前是否装有mysql
	命令：rpm -qa|grep -i mysql
	可以看到mysql的两个包：
	mysql-*..*.RHEL**
	mysqlclient*.RHEL**<br>
(3)、删除mysql
	删除命令：rpm -e --nodeps 包名
	( rpm -ev mysql-*.RHEL* )<br>
(4)、删除老版本mysql的开发头文件和库
	命令：rm -fr /usr/lib/mysql
	rm -fr /usr/include/mysql<br>
	注意：卸载后/var/lib/mysql中的数据及/etc/my.cnf不会删除，如果确定没用后就手工删除
	rm -f /etc/my.cnf
　　	rm -fr /var/lib/mysql

3.更改mysql密码：<br>
mysql > USE mysql;
mysql > delete from user where user=''; 
mysql > UPDATE user SET password = PASSWORD('新密码') WHERE user = 'root'; 
mysql > FLUSH PRIVILEGES;

4.修改mysql字符集：http://www.tuicool.com/articles/6b2Qvm

(1).set names utf8;<br>
(2).vim /etc/my.cnf 追加:<br>
	[client]<br>
	default_character_set=utf8<br>
	[mysql]<br>
	default_character_set=utf8<br>
	[mysqld]<br>
	default_character_set=utf8
	
(3).重启数据库服务：
	chkconfig --levels 235 mysqld on

	/etc/init.d/mysqld start

5.新建数据库：CREATE DATABASE `test2` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci

6.mysql导入mysql文件：

source /usr/local/tomcat/jiajiao.sql

7.远程连接数据库：

http://www.fantxi.com/blog/archives/enable-remote-access-mysql-centos/
- 具体如下：
	- ``` mysql -u root -p mysql # 第1个mysql是执行命令，第2个mysql是系统数据名称 ```
	- ``` grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option; ```
	- ``` flush privileges; exit;# 重载系统权限并退出 ```
	- ``` iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT ```
	- ``` service iptables save #保存防火墙配置 ```
	- ``` /etc/init.d/mysqld restart #重启MySQL```

<h4>3.redis配置相关</h4>

1、通过ps -ef|grep redis命令查看Redis进程；<br>
2、开启Redis服务操作通过/etc/init.d/redis_6379 start命令，也可通过（service redis_6379 start）；<br>
3、关闭Redis服务操作通过/etc/init.d/redis_6379 stop命令，也可通过（service redis_6379 stop）；<br>



<h4>4.安装PHP5.5</h4>

yum remove php  php-bcmath php-cli php-common  php-devel php-fpm    php-gd php-imap  php-ldap php-mbstring php-mcrypt php-mysql   php-odbc   php-pdo   php-pear  php-pecl-igbinary  php-xml php-xmlrpc
 
rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm
  
yum install php55w  php55w-bcmath php55w-cli php55w-common  php55w-devel php55w-fpm    php55w-gd php55w-imap  php55w-ldap php55w-mbstring php55w-mcrypt php55w-mysql   php55w-odbc   php55w-pdo   php55w-pear  php55w-pecl-igbinary  php55w-xml php55w-xmlrpc php55w-opcache php55w-intl php55w-pecl-memcache

目前php55w-mcrypt可能使用不了，可以考虑：


yum install php55w  php55w-bcmath php55w-cli php55w-common  php55w-devel php55w-fpm    php55w-gd php55w-imap  php55w-ldap php55w-mbstring php55w-mysql   php55w-odbc   php55w-pdo   php55w-pear  php55w-pecl-igbinary  php55w-xml php55w-xmlrpc php55w-opcache php55w-intl php55w-pecl-memcache


重启centos：
shutdown -r now 立刻重启(root用户使用)

正则表达式验证：
http://mp.weixin.qq.com/s?__biz=MjM5ODI5Njc2MA==&mid=2655807432&idx=1&sn=6ee6af53f1fbaee19960446afba1b575&scene=0

<h4>5.git 教程相关</h4>
- [教程1](http://www.yiibai.com/git/git_pull.html)
- [30分钟git命令入门](http://mp.weixin.qq.com/s?__biz=MjM5OTA1MDUyMA==&mid=2655436216&idx=1&sn=07cb1ceab6cf16fdf311d801739563b3&scene=23&srcid=0629eCqdpgkfEhljVPB6Iork#rd)
- [手把手教你用Git](http://mp.weixin.qq.com/s?__biz=MjM5OTA1MDUyMA==&mid=403636269&idx=2&sn=62d8327286c6ca8bd8898f51755ecdba&scene=21#wechat_redirect)
- [github上Fork 别人的项目后的常用的操作指南](http://it.taocms.org/10/5831.htm)
- [Git Push 免输用户名和密码](http://www.jianshu.com/p/f54053afecf2)，这种方法是将用户名和密码存入cache，一定时间后会失效
- [git-ssh 配置和使用](https://segmentfault.com/a/1190000002645623)，永远不需要输入密码
- [官网配置ssh](https://help.github.com/articles/generating-an-ssh-key/)
- [git bash配置beyond compare](http://www.scootersoftware.com/support.php?zz=kb_vcs#gitwindows)，先安装beyond compare，[beyond compare下载地址](http://www.scootersoftware.com/download.php)，在git bash里面输入以下命令配置
	- 1：``` git config --global diff.tool bc ```
	- 2：``` git config --global difftool.bc.path "E:/software_install/beyond_compare/install/Beyond Compare 4/bcomp.exe" ```
	- 3：``` git config --global merge.tool bc ```
	- 4：``` git config --global mergetool.bc.path "E:/software_install/beyond_compare/install/Beyond Compare 4/bcomp.exe ```
	- 5：使用 ``` git difftool foofile.txt ``` 查看foofile.txt与HEAD版本的差异
	- 6：使用 ``` git mergetool foofile.txt ``` merge foofile.txt文件

## Linux常见命令：
