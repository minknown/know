# kafka
本文介绍了kafka在linux服务器和java\php上的实现，以及可视化Web管理工具的EFAK的安装和运行。  
kafka官网：https://kafka.apache.org/  
EFAK官网：https://www.kafka-eagle.org/  
视频教程： https://b23.tv/Vb57Jhd  
kafka的应用场景：应用解耦、削峰填谷、活动跟踪和日志收集、流任务处理(发短信)等。  
kafka的学习扩展：配置名解释、分区概念、集群（zookeeper\hadoop）、重载数据积压消息不丢失等问题  

## kafka的安装
内存最低4GB,为重磁盘型应用，否则会由各种错误，  
不建议在Win下搭建kafka，除了错误较多，win本身也不适合做服务器,  
本案例使用Centos7，另外就是kafka的搭建前系统需要有java8+(jdk，可以不配JAVA_HOME)  
kafka安装为绿色解压缩安装方式，这里假设它位于root/kafka下，配置的话注意broker.id的唯一性。  
````
sudo yum install -y java-1.8.0-openjdk*-devel
chmod +x /root/kafka/bin/zookeeper-server-start.sh
chmod +x /root/kafka/bin/kafka-run-class.sh
/root/kafka/bin/zookeeper-server-start.sh /root/kafka/config/zookeeper.properties
chmod +x /root/kafka/bin/kafka-server-start.sh
/root/kafka/bin/kafka-server-start.sh /root/kafka/config/server.properties
````
通过java自带的jps命令，判断kakfa是否运行成功。

## kafka的实现
做配置并导入依赖,此处假设tasks为主题名字
````java
spring.kafka.bootstrap-servers=64.176.54.197:9092
<dependency>
<groupId>org.springframework.kafka</groupId>
<artifactId>spring-kafka</artifactId>
</dependency>
````

对于生产者
````java
@Autowired
private KafkaTemplate<String,String> xxx;
xxx.send("tasks","hello");
````

对于消费者
````java
@KafkaListener(topics = "tasks")
    public void  onMsf(ConsumerRecord<String,String> record){
        System.out.println("收到："+record.value());
    }
````
**踩坑**  
UnknownHostException异常：kafka的server.properties配置中加入listeners=PLAINTEXT://外网IP:9092，如果保存空则自动使用内网IP。 如果不行研究etc/hosts  
准确来讲是加入advertised.listeners。  
两者的不同：http://t.csdn.cn/00MZg  

## efak的实现
efak安装为绿色解压缩安装方式，这里假设它位于root/kafkaweb下，启动命令为bin/sk.sh start，配置文件为conf下system-config.properties，注意：
````
efak.zk.cluster.alias=cluster1
cluster1.zk.list=localhost:2181 //配置集群和zk的地址和端口
kafka mysql jdbc driver address //配置数据库，可使用宝塔快速安装mysql。

//需要配环境变量:vim /etc/profile（生效source /etc/profile）
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.382.b05-1.el7_9.x86_64
export JRE_HONE=$JAVA_HOME/jre
export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export KE_HOME=/root/kafkaweb
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$KE_HOME/bin:$PATH
````
**踩坑**  
注意关闭防火墙：systemctl stop firewalld;  
登录不上：ERROR - Telnet has error, msg is java.lang.IllegalArgumentException: port out of range:-1  
原因:和JAVA-JMX有关系，启动kafka时命令改为：JMX_PORT=6666 /root/kafka/bin/kafka-server-start.sh /root/kafka/config/server.properties或修改kafka-run-class.sh中JAVA-JMX的配置。  
可通过日志logs/error.log查看具体错误原因。也可到数据库查看是否存在ke库检查数据库是否存在问题。  


