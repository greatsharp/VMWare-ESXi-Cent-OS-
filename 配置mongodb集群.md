# 1.分别在三台server上创建sharding复制集 rs0, rs1, rs2 
172.18.195.14上创建rs0
>#./bin/mongod --port 27017 --dbpath=/opt/mongodb/data/db --logpath=/opt/mongodb/data/log/rs0-1.log --logappend --fork --shardsvr --replSet=rs0 --noauth --bind_ip_all  
>#./bin/mongod --port 27018 --dbpath=/opt/mongodb/data/db1 --logpath=/opt/mongodb/data/log/rs0-2.log --logappend --fork --shardsvr --replSet=rs0 --noauth --bind_ip_all  
>#./bin/mongo 172.18.195.14:27017  
> \>rs.initiate({_id: 'rs0', members: [{_id: 0, host: '172.18.195.14:27017'}, {_id: 1, host: '172.18.195.14:27018'}]})  
> \>rs.isMaster()  

![image](https://github.com/greatsharp/VMWare-ESXi-Cent-OS-/blob/master/images/mongodb%E5%88%9B%E5%BB%BA%E5%A4%8D%E5%88%B6%E9%9B%86.png)

172.18.195.10上创建rs1

172.18.195.16上创建rs2

# 2.分别在三台server上创建config服务，然后创建config复制集
>#./bin/mongod --port 27100 --dbpath=/opt/mongodb/data/conf --logpath=/opt/mongodb/data/log/config.log --logappend --fork --configsvr --replSet=conf --bind_ip_all  
>#./bin/mongo 172.18.195.10:27100  
> \>rs.initiate({_id: 'conf', members: [{_id: 0, host: '172.18.195.10:27100'}, {_id: 1, host: '172.18.195.14:27100'}, {_id: 2, host: '172.18.195.16:27100'}]})  
> \>rs.isMaster()

# 3.创建Route
>#nohup ./bin/mongos --port 40000 --configdb conf/172.18.195.10:27100,172.18.195.14:27100,172.18.195.16:27100 --fork --logpath=/opt/mongodb/data/log/route.log --logappend &  


# 4.设置分片  
>#./bin/mongo localhost:40000  
> \>use admin  
> \>db.runCommand({ addshard: 'rs0/172.18.195.14:27017,172.18.195.14:27018'})  
> \>db.runCommand({ addshard: 'rs1/172.18.195.10:27017,172.18.195.10:27018'})  
> \>db.runCommand({ addshard: 'rs2/172.18.195.16:27017,172.18.195.16:27018'})  
> \>db.runCommand({ enablesharding: 'test'})  
> \>db.runCommand({ shardcollection: 'test.user', key: {name:1}})
