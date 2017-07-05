# HOST
```
[root@iZwz95v28cjpudhp2sikufZ ~]# hostctl status
-bash: hostctl: δ�ҵ�����
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
> ��7�汾�У�hostname��������ʽ
> 
> ��̬(Static host name)
> 
> ��̬(Transient/dynamic host name)
> 
> ����(Pretty host name)
> 
>  
> 
> ��ѯ������
> 
> hostnamectl��hostctl status ��ѯ������
> hostnamectl status [--static|--transient|--pretty]

> �޸�hostname
> hostnamectl set-hostname servername [--static|--transient|--pretty]
> 
> ɾ��hostname
> 
> hostnamectl set-hostname ""
> hostnamectl set-hostname "" --static
> hostnamectl set-hostname "" --pretty
> 

> �޸������ļ�
> hostname  name
> vim /etc/hostname 
> 
> ͨ��nmtui�޸ģ�֮������hostnamed
> 
> systemctl restart systemd-hostnamed
> 

> ͨ��nmcui�޸ģ�֮������hostnamed
> nmcli general hostname servername
> systemctl restart systemd-hostnamed
> 
> ====================================
> 
> adduser myself  passwd mysqlf
> chmod -v u+w /etc/sudoers vim /etc/sudoers
> Allow root to run any commands anywher   root    ALL=(ALL)       ALL   myself  ALL=(ALL)       ALL  #������������û�
> 
> chmod -v u-w /etc/sudoers

# MYSQL
## ����mysqlԴ��װ��
shell> wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
## ��װmysqlԴ
shell> yum localinstall mysql57-community-release-el7-8.noarch.rpm

## ���
shell> yum repolist enabled | grep "mysql.*-community.*"

## ��װ
shell> yum install mysql-community-server

## ����
shell> systemctl start mysqld


car /var/log/mysqld.d������ ��ʱ�򿴲���
====�޸�/etc/my.cnf���� [mysqld] С�������һ�У�skip-grant-tables=1

��һ�������� mysqld ����ʱ�������������֤


2������mysqld ����systemctl restart mysqld


3��ʹ�� root �û���¼�� mysql��mysql -uroot 


4���л���mysql���ݿ⣬���� user ��

update user set authentication_string = password('123456'),password_expired = 'N', password_last_changed = now() where user = 'root';

��֮ǰ�İ汾�У������ֶε��ֶ����� password��5.7�汾��Ϊ�� authentication_string


5���˳� mysql���༭ /etc/my.cnf �ļ���ɾ�� skip-grant-tables=1������


6������mysqld ���������������¼����



wget http://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz

    tar -zxvf Python-3.6.0.tar
 �����ѹ������ļ���

    cd Pytho___<tab>

�ڱ���ǰ����/usr/local��һ���ļ���python3����Ϊpython�İ�װ·�������⸲���ϵİ汾��,��Ҫʹ��sudoȨ��

    mkdir /usr/local/python3

��ʼ���밲װ

    ./configure --prefix=/usr/local/python3
    make
    make install

    --prefix=/usr/local/python3����makefile�ļ������а�װĿ¼��linux�µİ�װ���Ǳ������Ӻ��ļ�������ϵͳ·���У�ָ����make�ͻ��������makefile�е�Ŀ���ļ���make installִ��makefile�еİ�װѡ���ɰ�װ��

��ʱû�и����ϰ汾���ٽ�ԭ��/usr/bin/python���Ӹ�Ϊ�������

    mv /usr/bin/python /usr/bin/python_old

�ٽ����°汾python������

    ln -s /usr/local/python3/bin/python3 /usr/bin/python

���ʱ������

    python   #�ͻ���ʾ��python���°汾��Ϣ
    Python 3.1.2 (r312:79147, Oct 21 2012, 01:03:21))
    [GCC 3.2.2 20030222 (Red Hat Linux 3.2.2-5)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

����������°�װ·��python3������ֱ��Ĭ�ϰ�װ����װ�����pythonӦ�ûḲ��linux���Դ����ϰ汾��Ҳ�п��ܲ����ǣ����忴��װ�����ˣ������ҿ����Լ������£���Ȼ������뱣��ԭ���İ汾����ô���ַ�����ò����ˡ�

������ʹpython2��python3���棬Ҳ���ǲ�Ҫ�޸��ϰ汾�����֣������°汾������������Ϊpython3��

    ln -s /usr/local/python3/bin/python3 /usr/bin/python3

����������python������ϰ汾������python3������°汾�����߹��棬����ʹ��
	

	��CentOS ��װeasy_install��pip�ķ���            

CentOS ��װeasy_install�ķ�����

wget -q http://peak.telecommunity.com/dist/ez_setup.py
python ez_setup.py
8��CentOS��װpython������װ����pip�ķ������£�

wget --no-check-certificate https://github.com/pypa/pip/archive/1.5.5.tar.gz

ע�⣺wget��ȡhttps��ʱ��Ҫ���ϣ�--no-check-certificate

tar zvxf 1.5.5    #��ѹ�ļ�
cd pip-1.5.5/
python3 setup.py install

OK�������Ͱ�װ��pip�ˣ�

**PS  ��ֹʹ�� wget ��װLinux��Anaconda ��װ��; ��������ܶ�Python ���İ�װ��**
��װ����ȱ��bzip2��
yum install -y bzip2


apache2 

mysql ----Զ������
��������ֱ����Ȩ(�Ƽ�)

�������κ�������ʹ��root�û������룺youpassword�����root���룩���ӵ�mysql��������

# mysql -u root -proot 
mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'youpassword' WITH GRANT OPTION;

��������м�ִ����������ˢ��Ȩ�� 

FLUSH PRIVILEGES 


## wsgi

```
 yum install -y httpd-devel
pip3 install mod_wsgi
```

###  �ӽ��� mod_wsgi ����
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
#################### ���� #### vim /etc/ /config''

cd  /etc/ld.so.conf.d
vim python3.conf >>>+++ /anaconda3/python3
ldconfig 
```

=====================ERROR====================
 1074  vim /etc/ld.so.conf
 1075  ldconfig
 �����������shared; No module named encoding; mod_wsgiҪ��Դ������shared���롣4.5.15

```
 ./configure --prefix=/home/myself/anaconda3/python3.5 --enable-shared    --enable-loadable-sqlite-extensions
```

=====No slotmem from mod_heartmonitor---======

��Щ��Ϣ���޹صġ�ͨ����������mod_heartmonitor�ġ�AH02282��No slotmem����Ϣ��ʵ���ϲ����Ǵ��󣩣�����Ȼ��һ�����������ķ�������

**PS** ͨ����������ͨ����httpd.confע����������ƽ��������ģ������ֹ����Ϣ��������ʵ��ʹ�����������˽�����Ĭ�������н�����ã�����Ȼ��û�С�
```
LoadModule lbmethod_heartbeat_module modules / mod_lbmethod_heartbeat.so
```

> ��֤����Ȩģ��֮һ���ܵ��·������ܾ���������⡣�����Գ��Խ�����httpd.conf�еġ�auth����ͷ��ģ�飬�Լ����������е��κ����ơ�





