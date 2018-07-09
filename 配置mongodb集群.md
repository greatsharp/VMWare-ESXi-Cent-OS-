# 1.服务器规划  
![](https://github.com/greatsharp/VMWare-ESXi-Cent-OS-/blob/master/images/mongodb%E9%9B%86%E7%BE%A4.png)

服务器172.18.195.10   |	服务器172.18.195.14   | 服务器172.18.195.16  
mongos               |	mongos                |	mongos  
config server	       | config server          |	config server  
shard server1 主节点  |	shard server1 副节点	 | shard server1 仲裁  
shard server2 仲裁    | shard server2 主节点	  | shard server2 副节点  
shard server3 副节点  |	shard server3 仲裁    | shard server3 主节点  

端口分配:  
mongos:20000  
config:21000  
shard1:27001  
shard2:27002  
shard3:27003  


# 2.config server复制集配置

pidfilepath = /usr/local/mongodb/config/log/configsrv.pid  
dbpath = /usr/local/mongodb/config/data  
logpath = /usr/local/mongodb/config/log/congigsrv.log  
logappend = true  

bind_ip = 0.0.0.0  
port = 21000  
fork = true  

#declare this is a config db of a cluster;  
configsvr = true  

#副本集名称  
replSet=configs  

#设置最大连接数  
maxConns=20000


# 3.shard1,shard2,shard3分片复制集配置

pidfilepath = /usr/local/mongodb/shard1/log/shard1.pid  
dbpath = /usr/local/mongodb/shard1/data  
logpath = /usr/local/mongodb/shard1/log/shard1.log  
logappend = true  


bind_ip = 0.0.0.0  
port = 27001  
fork = true  
 
#副本集名称  
replSet=shard1  

 
#declare this is a shard db of a cluster;  
shardsvr = true  

maxConns=20000


# 4.mongos路由服务器配置
pidfilepath = /usr/local/mongodb/mongos/log/mongos.pid  
logpath = /usr/local/mongodb/mongos/log/mongos.log  
logappend = true  


bind_ip = 0.0.0.0  
port = 20000  
fork = true  


#监听的配置服务器,只能有1个或者3个 configs为配置服务器的副本集名字  
configdb = configs/172.18.195.10:21000,172.18.195.14:21000,172.18.195.16:21000  

 
#设置最大连接数  
maxConns=20000


# 5.启用分片
登录mongos  
mongo --port 20000  

#使用admin数据库  
use  admin  

#串联路由服务器与分配副本集  
sh.addShard("shard1/172.18.195.10:27001,172.18.195.14:27001,172.18.195.16:27001")  
sh.addShard("shard2/172.18.195.10:27002,172.18.195.14:27002,172.18.195.16:27002")  
sh.addShard("shard3/172.18.195.10:27003,172.18.195.14:27003,172.18.195.16:27003")  

#查看集群状态  
sh.status()或db.runCommand({listshards:1})  
![](https://github.com/greatsharp/VMWare-ESXi-Cent-OS-/blob/master/images/mongodb%E6%9F%A5%E7%9C%8Bshards%E7%8A%B6%E6%80%81.png)
