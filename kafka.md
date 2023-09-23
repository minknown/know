# kafka
本文介绍了kafka在linux和java上的实现，以及可视化Web工具的EFAK的安装和运行。
kafka官网：https://kafka.apache.org/
EFAK官网：https://www.kafka-eagle.org/
## kafka的安装
不建议在Win下搭建kafka，除了错误较多，win本身也不适合做服务器,本案例使用Centos7，另外就是kafka的搭建前系统需要有java8+(jdk，可以不配JAVA_HOME)
kafka安装为绿色解压缩安装方式，这里假设它位于root/kafka下，配置的话注意broker.id的唯一性。
````
chmod +x /root/kafka/bin/zookeeper-server-start.sh
chmod +x /root/kafka/bin/kafka-run-class.sh
/root/kafka/bin/zookeeper-server-start.sh /root/kafka/config/zookeeper.properties
chmod +x /root/kafka/bin/kafka-server-start.sh
/root/kafka/bin/kafka-server-start.sh /root/kafka/config/server.properties
````
通过java自带的jps命令，判断kakfa是否运行成功。

## kafka
