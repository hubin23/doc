## 2017年8月3号
Markdown中的换行：  
空格空格＋回车

## 2017年8月11号
抛出service中捕获的异常，这样，外层才能捕获异常。

```java
//用这种方式，当Object为String类型时，会产生类型转换异常
(boolean)Object == true;

//用这种方式，则不会有问题
Boolean.parseBoolean(Object) == true;
```
***
Linux中快捷命令在 ~/.bashrc 中创建  
vi ~/.bashrc 即可编辑。

***
对数据库中数据进行加减时，最好直接在sql中进行加减操作，防止并发，比如：  
UPDATE tablename SET column = column + addition;

***
### github操作相关命令
*git pull*：拉取  

*git commit .*：提交  

*git push*：推送到服务器

*git branch*：查看分支情况

*git branch -a*：查看所有分支  

*git branch -r*：查看远端分支  

*git checkout branchname*：切换分支到branchname  

*git merge branchname*：合并branchname 到当前分支

## 2018年7月6号
在服务器上搭建shadowsocks服务

1、购买境外VPS服务。（暂用Vultr）

2、SSH登录VPS。

3、服务器上部署SS服务，网上有多种方法，整理如下：

a:依次执行以下命令：
```
$ yum install m2crypto python-setuptools
$ easy_install pip
$ pip install shadowsocks
```
安装完成后，编辑配置文件：
```
$ vi /etc/shadowsocks.json
```
一般使用多用户模式：
```
{
    "server":"此处为当前服务器IP",
    "local_address": "127.0.0.1",
    "local_port":1080,
    "port_password": {
         "分配端口1": "为端口1配置的密码",
         "分配端口2": "为端口2配置的密码"
     },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```
安装防火墙：
```
$ yum install firewalld
```
启动防火墙：
```
$ systemctl start firewalld
```
在防火墙中开启已在shadowsocks.json中配置的端口，“******”处为端口：
```
$ firewall-cmd --permanent --zone=public --add-port=******/tcp
$ firewall-cmd --reload
```
开启SS服务：
```
$ nohup ssserver -c /etc/shadowsocks.json &
```

至此，SS服务端搭建并启动完毕。

#### ONE MORE THING:
据说配合BBR服务更爽，依次执行以下命令：
```
$ wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh
$ chmod +x bbr.sh
$ ./bbr.sh
```
然后提示重启，按Y确认
