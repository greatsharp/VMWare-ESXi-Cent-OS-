# 1.服务器规划  
服务器172.18.195.10   |	服务器172.18.195.14   | 服务器172.18.195.16  
mongos               |	mongos                |	mongos  
config server	       | config server          |	config server  
shard server1 主节点  |	shard server1 副节点	 | shard server1 仲裁  
shard server2 仲裁    | shard server2 主节点	  | shard server2 副节点  
shard server3 副节点  |	shard server3 仲裁    | shard server3 主节点  

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
