# HOST
```
[root@iZwz95v28cjpudhp2sikufZ ~]# hostctl status
-bash: hostctl: 未找到命令
[root@iZwz95v28cjpudhp2sikufZ ~]# hostnamectl
   Static hostname: iZwz95v28cjpudhp2sikufZ
         Icon name: computer-vm
           Chassis: vm
        Machine ID: 7d26c16f128042a684ea474c9e2c240f
           Boot ID: 1a7a794ac5db4f07b54136317c5fbd0f
    Virtualization: kvm
  Operating System: CentOS Linux 7 (Core)
       CPE OS Name: cpe:/o:centos:centos:7
            Kernel: Linux 3.10.0-327.36.3.el7.x86_64
      Architecture: x86-64
```


>  hostnamectl
> 
> 在7版本中，hostname有三种形式
> 
> 静态(Static host name)
> 
> 动态(Transient/dynamic host name)
> 
> 别名(Pretty host name)
> 
>  
> 
> 查询主机名
> 
> hostnamectl或hostctl status 查询主机名
> hostnamectl status [--static|--transient|--pretty]

> 修改hostname
> hostnamectl set-hostname servername [--static|--transient|--pretty]
> 
> 删除hostname
> 
> hostnamectl set-hostname ""
> hostnamectl set-hostname "" --static
> hostnamectl set-hostname "" --pretty
> 

> 修改配置文件
> hostname  name
> vim /etc/hostname 
> 
> 通过nmtui修改，之后重启hostnamed
> 
> systemctl restart systemd-hostnamed
> 

> 通过nmcui修改，之后重启hostnamed
> nmcli general hostname servername
> systemctl restart systemd-hostnamed
> 
> ====================================
> 
> adduser myself  passwd mysqlf
> chmod -v u+w /etc/sudoers vim /etc/sudoers
> Allow root to run any commands anywher   root    ALL=(ALL)       ALL   myself  ALL=(ALL)       ALL  #这个是新增的用户
> 
> chmod -v u-w /etc/sudoers

# MYSQL
## 下载mysql源安装包
shell> wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
## 安装mysql源
shell> yum localinstall mysql57-community-release-el7-8.noarch.rpm

## 检查
shell> yum repolist enabled | grep "mysql.*-community.*"

## 安装
shell> yum install mysql-community-server

## 启动
shell> systemctl start mysqld


car /var/log/mysqld.d。。。 有时候看不到
====修改/etc/my.cnf，在 [mysqld] 小节下添加一行：skip-grant-tables=1

这一行配置让 mysqld 启动时不对密码进行验证


2、重启mysqld 服务：systemctl restart mysqld


3、使用 root 用户登录到 mysql：mysql -uroot 


4、切换到mysql数据库，更新 user 表：

update user set authentication_string = password('123456'),password_expired = 'N', password_last_changed = now() where user = 'root';

在之前的版本中，密码字段的字段名是 password，5.7版本改为了 authentication_string


5、退出 mysql，编辑 /etc/my.cnf 文件，删除 skip-grant-tables=1的内容


6、重启mysqld 服务，再用新密码登录即可



wget http://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz

    tar -zxvf Python-3.6.0.tar
 进入解压缩后的文件夹

    cd Pytho___<tab>

在编译前先在/usr/local建一个文件夹python3（作为python的安装路径，以免覆盖老的版本）,需要使用sudo权限

    mkdir /usr/local/python3

开始编译安装

    ./configure --prefix=/usr/local/python3
    make
    make install

    --prefix=/usr/local/python3生成makefile文件，其中安装目录（linux下的安装就是编译链接后将文件拷贝到系统路径中）指定，make就会编译链接makefile中的目标文件，make install执行makefile中的安装选项，完成安装。

此时没有覆盖老版本，再将原来/usr/bin/python链接改为别的名字

    mv /usr/bin/python /usr/bin/python_old

再建立新版本python的链接

    ln -s /usr/local/python3/bin/python3 /usr/bin/python

这个时候输入

    python   #就会显示出python的新版本信息
    Python 3.1.2 (r312:79147, Oct 21 2012, 01:03:21))
    [GCC 3.2.2 20030222 (Red Hat Linux 3.2.2-5)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

如果不建立新安装路径python3，而是直接默认安装，则安装后的新python应该会覆盖linux下自带的老版本，也有可能不覆盖，具体看安装过程了，这个大家可以自己试验下，当然如果还想保留原来的版本，那么这种方法最好不过了。

还可以使python2和python3共存，也就是不要修改老版本的名字；创建新版本的名字是命名为python3。

    ln -s /usr/local/python3/bin/python3 /usr/bin/python3

这样，输入python会进入老版本；输入python3会进入新版本，两者共存，则需使用
	

	、CentOS 安装easy_install、pip的方法            

CentOS 安装easy_install的方法：

wget -q http://peak.telecommunity.com/dist/ez_setup.py
python ez_setup.py
8、CentOS安装python包管理安装工具pip的方法如下：

wget --no-check-certificate https://github.com/pypa/pip/archive/1.5.5.tar.gz

注意：wget获取https的时候要加上：--no-check-certificate

tar zvxf 1.5.5    #解压文件
cd pip-1.5.5/
python3 setup.py install

OK，这样就安装好pip了，

**PS  截止使用 wget 安装Linux的Anaconda 安装包; 可以免掉很多Python 包的安装。**
安装容易缺少bzip2包
yum install -y bzip2


apache2 

mysql ----远程连接
方法二、直接授权(推荐)

　　从任何主机上使用root用户，密码：youpassword（你的root密码）连接到mysql服务器：

# mysql -u root -proot 
mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION;

操作完后切记执行以下命令刷新权限 

FLUSH PRIVILEGES 


## wsgi

```
 yum install -y httpd-devel
pip3 install mod_wsgi
```

###  子进程 mod_wsgi 覆盖
### No module Python_path

```
echo 'Python 3.5.2 is not installed, installing Python 3 pre-requisites...'
yum -y groupinstall development

echo 'Installing extra packages for Python...'
yum -y install zlib-devel openssl-devel sqlite-devel bzip2-devel python-devel openssl-devel libffi-devel openssl-perl libjpeg-turbo-devel zlib-devel giflib ncurses-devel gdbm-devel xz-devel tkinter readline-devel tk tk-devel

echo 'Installing Python 3.5.2...'
wget -q 'https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tgz'
tar -xzf 'Python-3.5.2.tgz'
cd ./Python-3.5.2
CXX=g++ ./configure --enable-shared
make

echo 'Moving to alternate location to keep system Python version intact...'
make altinstall
cd ..
rm Python-3.5.2.tgz
rm -rf ./Python-3.5.2
ln -fs /usr/local/bin/python3.5 /usr/bin/python3.5
echo "/usr/local/lib/python3.5" > /etc/ld.so.conf.d/python35.conf
echo "/usr/local/lib" >> /etc/ld.so.conf.d/python35.conf
ldconfig

echo 'Now, install mod_wsgi...'
wget -q "https://github.com/GrahamDumpleton/mod_wsgi/archive/4.4.21.tar.gz"
tar -xzf '4.4.21.tar.gz'
cd ./mod_wsgi-4.4.21
./configure --with-python=/usr/local/bin/python3.5
make
make install
```


## ldd /etc/httpd/modules/mod_wsgi.so
=======mod_wsgi4.5.15

```
make distclean
./configure --with-python=/usr/local/bin/python3.5
LD_RUN_PATH=/usr/local/lib make
sudo make install
#################### 核心 #### vim /etc/ /config''

cd  /etc/ld.so.conf.d
vim python3.conf >>>+++ /anaconda3/python3
ldconfig 
```

=====================ERROR====================
 1074  vim /etc/ld.so.conf
 1075  ldconfig
 上面的问题解决shared; No module named encoding; mod_wsgi要用源码下载shared编译。4.5.15

```
 ./configure --prefix=/home/myself/anaconda3/python3.5 --enable-shared    --enable-loadable-sqlite-extensions
```

=====No slotmem from mod_heartmonitor---======

这些消息是无关的。通常遇到来自mod_heartmonitor的“AH02282：No slotmem”消息（实际上并不是错误），但仍然有一个运行正常的服务器。

**PS** 通常，您可以通过从httpd.conf注释心跳负载平衡器方法模块来禁止该消息（除非您实际使用它）。有人建议在默认配置中将其禁用，但显然还没有。
```
LoadModule lbmethod_heartbeat_module modules / mod_lbmethod_heartbeat.so
```

> 认证或授权模块之一可能导致服务器拒绝请求的问题。您可以尝试禁用以httpd.conf中的“auth”开头的模块，以及您在配置中的任何限制。





