# 1.分别在三台server上创建sharding复制集  
>#./bin/mongod --port 27017 --dbpath=/opt/mongodb/data/db --logpath=/opt/mongodb/data/log/rs0-1.log --logappend --fork --shardsvr --replSet=rs0 --noauth --bind_ip_all  
>#./bin/mongod --port 27018 --dbpath=/opt/mongodb/data/db1 --logpath=/opt/mongodb/data/log/rs0-2.log --logappend --fork --shardsvr --replSet=rs0 --noauth --bind_ip_all  
>#./bin/mongo 172.18.195.14:27017  
> !>rs.initiate({_id: 'rs0', members: [{_id: 0, host: '172.18.195.14:27017'}, {_id: 1, host: '172.18.195.14:27018'}]})  
>rs.isMaster()

