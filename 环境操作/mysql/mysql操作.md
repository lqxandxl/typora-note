# centos7安装mysql

查询mariadb并删除。

```
rpm -qa|grep maria、
rpm -e --nodeps  全称
```

安装

```
安装yum repository。
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
//yum -y install mysql-community-server
yumdownloader --resolve --destdir=/root/mysqlsrc/ mysql-community-server
```

copy至内网后，

```
rpm -ivh mysql*
```

数据库初始化

```
mysql_install_db --datadir=/var/lib/mysql
//为datadir指定所属。
chown -R mysql:mysql /var/lib/mysql/
vi /etc/my.cnf
//忽视表名大小写 加入一行
lower_case_table_names=1
```

启动服务

```
service mysqld start
查看默认密码
cat ~/.mysql_secret
mysql -uroot -p 输入查到的密码
set password=password('123456');
```

修改密码

```
//进入mysql所在机器
mysql -uroot -p 连接，输入密码
set password=password('chaosblade@2022');
```

开启远程权限

```
use mysql;
Update user set host='%' where user='root';
Flush privileges;
```

