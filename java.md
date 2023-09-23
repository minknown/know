## Java安装，在WINDOWS上
https://www.oracle.com/sg/java/technologies/downloads/  
https://www.java.com/zh-CN

## Java安装，在Centos上
````
java8:sudo yum install -y java-1.8.0-openjdk*-devel  
java17:sudo yum install java-17-openjdk*-devel  
//注意：尾部加-devel才代表JDK，紧跟openjdk，*一般可以去除。  
````
> 通过java -version验证安装。  
> 通过which java（推荐方法：在ls -lrt dir进入多层直到找到）、find / -name 'java'、whereis java查找jdk安装的位置。  
> 通过yum search java | grep java 搜索java的所有软件包。  

## 环境变量  
JAVA_HOME和JRE_HOME   
PATH加入上述两个bin即可。  
````java
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.372.b07-1.el7_9.x86_64
export JRE_HONE=$JAVA_HOME/jre
export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH
````
快速生效:source /etc/profile,echo $JAVA_HOME


## 卸载方法
由于EPICS工作环境下安装CSS，但CSS不支持开源jdk,所以首先需要卸载open jdk,然后再安装jdk-8u144-linux-x64.tar.gz（CSS只支持8及以上版本）。

一、卸载，需卸载干净，不然会出各种覆盖问题，很麻烦！

安装好的CentOS会自带OpenJdk,用命令 java -version ，会有下面的信息：

java version "1.6.0"
OpenJDK  Runtime Environment (build 1.6.0-b09)
OpenJDK 64-Bit Server VM (build 1.6.0-b09, mixed mode)

最好还是先卸载掉openjdk,在安装sun公司的jdk.

先查看 rpm -qa | grep java

显示如下信息：

java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

卸载：

rpm -e --nodeps java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
rpm -e --nodeps java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

还有一些其他的命令

rpm -qa | grep gcj

rpm -qa | grep jdk

如果出现找不到openjdk source的话，那么还可以这样卸载

 yum -y remove java java-1.4.2-gcj-compat-1.4.2.0-40jpp.115
 yum -y remove java java-1.6.0-openjdk-1.6.0.0-1.7.b09.el5

卸载完成后，可以用以下方法检验有没有卸载干净，如没有，继续卸载：

1）、查看Jdk的安装路径：

whereis java
which java （java执行路径）
echo $JAVA_HOME

echo $PATH

二、安装

卸载完成后，就需要安装了：

1）下载jdk，小编这里使用的是jdk-8u144-linux-x64.tar.gz版本

2）新建一个jdk的安装路径，我是在usr/local目录下新建java目录，指令如下：

mkdir /usr/local/java3）把下载的jdk-8u144-linux-x64.tar.gz包拷贝到新建的java目录下：
cp jdk-8u144-linux-x64.tar.gz /usr/local/java

4）进入到java目录，解压：

tar -xzvf jdk-8u144-linux-x64.tar.gz
5)进入java目录下的/etc/profile,编辑profile (vim /etc/profile),配置环境变量：

在profile文件的末尾加入如下命令行配置：

export JAVA_HOME=/usr/local/java/jdk1.8.0_144export JRE_HOME=/usr/local/java/jdk1.8.0_144/jre export PATH=$PATH:/usr/local/java/jdk1.8.0_144/生动的月亮 export CLASSPATH=./:/usr/local/java/jdk1.8.0_144/lib:/usr/local/java/jdk1.8.0_144/jre/lib然后：wq推出，并source profile,使刚才的配置生效

6)然后用java -version检查，就会出现java刚才安装的版本信息，则成功！

遇到问题又来重新追加！！！！！

我已经装了将java,环境等也配置成功了，第一次也可以使用CSS，但是当我再次打开时，出现如下问题：

A Java Runtime Environment (JRE) or Java Development Kit (JDK)

must be available in order to run STS. No Java virtual machine

was found after searching the following locations:

/home/carlos/Documents/soft/sts-bundle/sts-3.7.0.RELEASE/jre/生动的月亮/java

java in your current PATH

解决方法：

进入我的sts(css)的安装目录，就是/home/carlos/Documents/soft/sts-bundle/sts-3.7.0.RELEASE，然后，执行下面命令：

/home/carlos/Documents/soft/sts-bundle/sts-3.7.0.RELEASE

mkdir jre

cd jre

ln -s 你的JDK安装目录/生动的月亮 生动的月亮

即给sts创建jre,并将JDK安装目录下的生动的月亮在sts的jre下建立软连接

(关于为什么第一次可以运行，我也没想明白，欢迎指导，谢谢)



参考网址：

1）https://www.cnblogs.com/dingjiaoyang/p/5102827.html

2）http://m.blog.csdn.net/ILV_XJ/article/details/78120520

3）http://www.aichengxu.com/java/10682726.htm

