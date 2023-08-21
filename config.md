
## 常用配置

For mysql
````
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://bdm291915593.my3w.com:3306/bdm291915593_db
spring.datasource.username=bdm291915593
spring.datasource.password=password
*//spring.datasource.type=com.alibaba.druid.pool.DruidDataSource*
*//com.mysql.jdbc.Driver OR com.mysql.cj.jdbc.Driver*
*//?useUnicode=true&characterEncoding=utf-8&useSSL=false&serverTimezone=UTC*

````

For redis
````
logging.config.com.mayizt.redis=off
spring.redis.host=127.0.0.1
spring.redis.port=6379
spring.redis.password=123456
spring.redis.lettuce.pool.max-active=8
spring.redis.lettuce.pool.max-idle=8
spring.redis.lettuce.pool.max-wait=100
spring.redis.lettuce.pool.min-idle=0
````
