# CentOS学习笔记

## yum
Yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装

## CentOS部署Node.js程序
### 安装Node.js
#### 用yum安装gcc
```powershell
yum -y install gcc make gcc-c++ openssl-devel wget
```

#### 安装Node.js v9.4.0
1. 开始安装Node.js，先进入`/usr/src`文件夹，这个文件夹通常用来存放软件源代码:
```powershell
cd /usr/src
```

2. 从Node.js的站点中获取压缩档源代码
```powershell
wget https://nodejs.org/dist/v9.4.0/node-v9.4.0.tar.gz

```
3. 然后解压提取文件
```powershell
tar zxvf node-v9.4.0.tar.gz         # tar -xvfz node-v9.4.0.tar.gz 解压一个gzip格式的压缩包
```

4. 执行后会生成node-v9.4.0文件夹，cd进入,里面有个configure文件，配置并编译#这步执行得比较久，可以先去喝杯咖啡
```powershell
cd node-v9.4.0
./configure
make
```

5. 安装
```powershell
make install
```

6. 最后使用`node -v`检查是否安装成功。

### 安装MongoDB
1. 配置包管理系统（yum）：创建一个`/etc/yum.repos.d/mongodb-org-3.6.repo`文件，这样你就可以直接使用yum来安装MongoDB。
```powershell
cd /etc/yum.repos.d
vi mongodb-org-3.6.repo         # 进入vi的一般模式
# 在一般模式之中，只要按下 i, o, a 等字符就可以进入输入模式了！
# 在编辑模式当中，你可以发现在左下角状态栏中会出现 –INSERT- 的字样，那就是可以输入任意字符的提示。
```
把下列内容保存至`mongodb-org-3.6.repo`中
```powershell
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
```
按`ESC`键回到vi一般模式后，按`:wq`保存退出

2. 安装MongoDB服务器：
```powershell
# yum install mongodb-org -y
```
安装完成用`mongod --version`查看版本

3. MongoDB的基本操作：
```powershell
service mongod start            # 启动MongoDB
service mongod stop             # 停止MongoDB
service mongod restart          # 重启MongoDB
mongo                           # MongoDB shell
```


## CentOS设置相关
### CentOS安装五笔输入法
1. 加开终端，输入`su root`，再输入密码。
2. 登录root后，再键入`yum remove ibus`，移除现有的输入法框架。移除过程中会弹出询问是否真的移除，输入`y`继续。
3. 移除完毕后，再键入`yum install ibus ibus-table`，回车后重新安装输入法框架。同样，在执行过程中会询问是否确认安装，键入`y`回车继续。
4. 输入`yum install ibus ibus-table-wubi`安装极点五笔输入法，并且在执行过程中键入`y`确认下载和安装。
5. 安装成功后，键入`exit`退出root帐号，然后再关闭终端窗口。
6. 在`设置 > 区域和语言`中添加输入源。如果没有出现五笔则重启CentOS。

## Hyper-v相关
虚拟机和系统之前鼠标切换用：`ctrl + alt + ← `

## 相关链接
- [CentOS 7部署Node.js+MongoDB：在VPS上从安装到Hello world](http://blog.csdn.net/azureternite/article/details/52349326)
- [CentOS 新建、删除、移动、复制等命令](http://blog.csdn.net/lpdx111/article/details/16877725)
