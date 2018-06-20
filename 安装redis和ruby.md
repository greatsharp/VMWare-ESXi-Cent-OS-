1. redis的安装与配置请参考https://blog.csdn.net/ludonqin/article/details/47211109

2. 安装ruby  
#curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -  
#curl -L get.rvm.io | bash -s stable  
#source /usr/local/rvm/scripts/rvm  
#rvm install 2.3.3  
#rvm use 2.3.3  
#ruby --version  
#gem install redis


3. redis集群配置常见https://blog.csdn.net/jek123456/article/details/72518002

4. 关闭centos 7的防火墙  
#systemctl stop firewalld.service  
#systemctl disable firewalld.service 
