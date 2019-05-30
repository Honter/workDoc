# Linux部署SVN

* 1.连接服务器
```
ssh root@192.168.1.1 (部署的服务器地址)
```
输入密码

* 2.安装svn并创建版本库
进入主目录(项目文档位置/home/retina/svn)
安装svn
```
yum -y install subversion
```
创建版本库
```
cd /home/retian/svn
```
```
svnadmin create /home/retina/svn/项目名
```
 cd /项目  ls -a  如有conf等5类文件代表创建ok

 * 3.配置权限
 在2中目录位置/home/retina/svn/项目输入命令（一般建议放在home文件夹下，在新建一个文件夹存放）
 ```
 cd conf
 vi authz
 ```
 在文件最后输入
```
[\]
用户名1 = rm
用户名2 = rm
```
配置用户密码
```
vi passwd
```
在文件最后面输入
```
用户名 = 密码
```
svn配置
```
vi svnserver.conf
```
找到以下代码去掉注释#
```
anon-access=none
auth-access=write
Password-db = passwd
Realm = My First Prepository
```

* 4.根据cenos版本可自行百度关闭防火墙相关配置
centos6相关命令
```
/sbin/iptables -I INPUT -p tcp --dport 3690 -j ACCEPT
/etc/init.d/iptables save
service iptables restart
```
* 5.启动svn
```
svnserve -d -r /home/svn/仓库名
```
* 6.其他命令
查看svn安装位置
```
rpm -ql subversion
```
查看svn进程
```
ps -ef|grep svn|grep -v grep
```
关闭svn进程
```
 kill 端口号
```
查看进程命令返回结果如下：
root 12538 1 0 14:40 ? 00:00:00 svnserve -d -r /opt/svn/repositories
此进程对于的关闭命令为  kill 12538
