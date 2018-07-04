# 连接Redis集群的配置  
#REDIS (RedisProperties)  
#Redis数据库索引（默认为0）  
spring.redis.database=0  
#Redis集群配置  
spring.redis.cluster.nodes=172.18.195.14:30000,172.18.195.14:30001,172.18.195.10:30000,172.18.195.10:30001,172.18.195.16:30000,172.18.195.16:30001   
#连接池最大连接数（使用负值表示没有限制）  
spring.redis.pool.max-active=8  
#连接池最大阻塞等待时间（使用负值表示没有限制）  
spring.redis.pool.max-wait=-1  
#连接池中的最大空闲连接  
spring.redis.pool.max-idle=8  
#连接池中的最小空闲连接  
spring.redis.pool.min-idle=0  
#连接超时时间（毫秒）  
spring.redis.timeout=0  



# 如果是连接redis单机，更换如下配置  
#Redis服务器地址  
spring.redis.host=172.18.195.14  
#Redis服务器连接端口  
spring.redis.port=30000  
#Redis服务器连接密码（默认为空）  
spring.redis.password=123456  

