# jaryum

```
yum install yum-plugin-downloadonly
yum --downloadonly --downloaddir=/root/yumsrc install wget

```

# nc

查看指定ip和端口是否联通。

```
nc -vz ip port
```



# jar包解压和压缩命令

```
jar cvf test.jar test //压缩
jar xvf xx.jar //解压
```



# openssh-server安装

```
//前置内容安装
yum --downloadonly --downloaddir=/root/net-tools install net-tools
yum --downloadonly --downloaddir=/root/initscripts install initscripts
//openssh-server
yum --downloadonly --downloaddir=/root/openssh-server install openssh-server
//压缩
tar cf net-tools.tar net-tools
tar cf initscripts.tar initscripts
//传出
docker cp 7d5b98b5d4fb:/root/initscripts.tar /Users/liqixin/Downloads
docker cp 7d5b98b5d4fb:/root/net-tools.tar /Users/liqixin/Downloads

//对于initscripts来说，低版本centos7.4会有冲突 且需要rc
http://mirror.centos.org/centos/7/os/x86_64/Packages/bc-1.06.95-13.el7.x86_64.rpm
//为了解决冲突从历史版本中下载
initscripts-9.49.46-1.el7.x86_64.rpm //src.rpm包安装不管用 这个版本也提示冲突
//提示缺失mockbuild
groupadd mockbuild
useradd mockbuild -g mockbuild
//使用--nodeps --force安装
/usr/sbin/sshd-keygen -A
/usr/sbin/sshd 启动即可
```



# 查看操作系统版本

```
cat /etc/redhat-release
uname -r //内核
```

# rpm包地址

```
https://pkgs.org/
//历史rpm包 按名称和版本搜索即可
http://rpm.pbone.net/
```
