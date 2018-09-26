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


## 2018年9月26号

打包python为可执行exe文件

1：安装pyinstaller，默认为已设置好python环境变量，命令为：`pip install pyinstaller`，若未配置好python环境变量，则需要移动到python安装目录的scripts目录下，再执行安装命令

2: 安装pywin32，命令：`pip install pywin32`  

P.S. 查看已经安装的第三方库命令：`pip list`

3: 开始打包，`pyinstaller  -F  xxx.py`，其中-F为参数，可以写多个，如`pyinstaller.py -F -w  xxx.py`

P.S. 若需要修改程序图标：`pyinstaller.py -F -w -i "xxx.ico" "xxx.py"`，ico图标库：https://www.easyicon.net/

|参数|含义|
|---|---|
|-F|指定打包后只生成一个exe格式的文件|
|-D|–onedir 创建一个目录，包含exe文件，但会依赖很多文件（默认选项）|
|-c|–console, –nowindowed 使用控制台，无界面(默认)|
|-w|–windowed, –noconsole 使用窗口，无控制台|
|-p|添加搜索路径，让其找到对应的库。|
|-i|改变生成程序的icon图标|

