在CentOS6.8下安装Docker  

系统版本  

[root@bogon yum.repos.d]# uname -a  

Linux bogon 2.6.32-642.el6.x86_64 #1 SMP Tue May 10 17:27:01 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux  

[root@bogon yum.repos.d]# cat /etc/redhat-release   

CentOS release 6.8 (Final)  

安装EPEL  

因为系统自带的repo中不带docker需要安装epel  


rpm -Uvh http://ftp.riken.jp/Linux/fedora/epel/6Server/x86_64/epel-release-6-8.noarch.rpm  

安装Docker  

yum install -y docker-io  

开机自启动与启动Docker  

[root@bogon yum.repos.d]# service docker start  

Starting cgconfig service:                                 [  OK  ]  

Starting docker:                                       [  OK  ]  

[root@bogon yum.repos.d]# chkconfig docker on  

[root@bogon yum.repos.d]# chkconfig docker --list  

docker          0:off   1:off   2:on    3:on    4:on    5:on    6:off  


至此docker已经安装完成
