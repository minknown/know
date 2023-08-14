# know
存放近期要学习的点，辅助知识，核心知识，以及其他工具类和教程。

## 近期要学习的点
* druid
* 正向代理和反向代理
* kaka消息队列
* Springclound
* 英语和学历问题

## 核心知识-SQL

**ElasticSearch**  :*暂无*  
**Mysql**  
1. mysql懂得分区分表简单的优化。
2. 学习更多复杂的语句包括事务。

**Redis**
1. redis基础:默认内网，AUTH+密码，ping->pong
2. 懂得安装和应用场景，学会五个数据类型。
3. 应对数据持久化和缓存三大问题。
4. 集群部署方法:https://www.bilibili.com/video/BV1Pi4y157L1 *(哨兵模式被淘汰了)*

## 核心知识-kafka
写入...

## 核心知识-Mybaits

1. 做数据库的连接配置
2. 创建实体类、接口类
3. 在启动或测试类中注入接口类直接引用即可

* mybaits-config和UserMapper.xml建立了关系：（通过右键-COPY_PATH,By ser_root）
* 而userMapper.xml和接口建立了关系：（通过命名空间和语句id）
* 接口和usermapper.xml需要同个目录下，但ORM-xml警擦位于res目录，故新建目录时使用/
* 大部分代码：https://mybatis.org/mybatis-3/zh/getting-started.html
* 学会：plus\多参\注解开发 * 注意：mybaits-config中typeAliases可以设置扫面描后， resultType="User"无需填写包名
* 注意：在Main或者Boot-App入口，设置@MapperScan("com.mayizt.mapper")[接口目录],可避免找不到接口的错误
* 注意：mysql-connector-java:jar:unknown was not错误：在pom中为mysql驱动指定版本
  
## 辅助知识-Linux运维
* 服务器选型centos7.8(7.6-7.9)，可使用bt辅助。
* 能够了解目录接口，了解文件操作、基本地查看内存和用户、网络设置。
* com笔记版:tree,tail,cat\vim\启动服务，压缩tar/zip/rar。chmod提权/sh执行shell。shutdown -h now关机reboot重启。
* shell笔记版:{$x}变量，&>输出,[]运算，路径PATH/USER/time/$?，function,for,read p,echo颜色。ifthen(-eq -z -f)
* 服务：systemctl status/stop.start/disable.enable firewalld/httpd，ps -ef | grep name
* 备份：cron+tar即可
* 部署：apache\nginx\tomcat,对应目录htdoc\html\.webapps,目录提供错误访客日志,conf,bin.
* 安装前：sudo yum update,set firewalld. wget+JCC
* 安装中：http://nginx.org/en/linux_packages.html,yum install httpd,gar-tomcat(down:bin)
* 注意：tomcat安装方式为tar解压-->usr/local。且需要先安装JAVA+环境配置。

## 辅助知识-简单压测
* 使用阿里云压测，了解TPS\QPS\RT\SL（成功率稳定性）（压测成本10000/50元，比Jmeter有效且可以模拟多地多IP）
* 学会断言的用法，了解HTTP接口压测,HTTP多口压测,还支持APP、WEBSOCKET等压测。
* 压测时注意磁盘、内存、数据库、宽带的监测，已确定哪个是瓶颈，并发给开发者进行改善优化。
* tps：mysql->10000,redis->100000,磁盘内存用固态等新硬件，主要看带宽5万在线访客，一般100MBps。带宽贵。可使用CDN等加速服务。
* 压测目标的确定：
1. 10-20-30定律（10分钟是压测时间、取注册用户的20%为活跃，再取其30%作为最高并发）
2. 根据公司过往的TPS目标
3. 从服务项目监控系统、或者访问日志（绝对有），找到访问量最大的一天的最大峰值，精确到分钟，如晚上8点10分的最大调用量为12000，则tps=12000/60
4.根据二八定律，注册用户的80%来算，一天去除访问低段落如凌晨0-6点，还有18小时，用18小时乘以20%，为12960秒，则tps=80万/12960
5. 无法确定压测目标的，直接告诉压测结果，有领导等部门会议考虑决定拍板。

## 辅助知识-桌面程序
易语言：https://www.dywt.com.cn  
JAVA:JAVAFX(之前使用awt,后面swing,现在用javafx,就好像springboot淘汰了ssm一样)  
具体教程：https://www.bilibili.com/video/BV1W24y1y7wd  
scene-builder:https://openjfx.cn/scene-builder/#download  
exe4j:https://exe4j.apponic.com/  

## 其他-指定索引
1. 问题解决：LogorBug->Google->StackOverflow->QQ->CSDN->联络员
2. 网盘备份：Googdriver->Dropbox->ftpbox.org    
  *(前者最大15GB，后两者均为双向自动同步)*
3. 宣称协助工具：todesk、向日葵，电话使用微信或QQ等
4. VPM：https://m-n.cc/NzAIGFv
5. MAVEN:https://mvnrepository.com   
6. 镜像：暂无  


## 其他-工具箱
*(注意:HBuilderX实时预览md时加入charset=UTF-8解决中文乱码问题)* 

|工具箱名字|软件名|产品入口|说明|
|----|----|----|----|
|**EyeGreen**|小智护眼宝|https://huyanbao.cqttech.com |建议设置每1小时休息15分钟
|SSH|electerm|https://electerm.html5beta.com |支持SFTP等
|FTP|8uftp|http://www.8u.cn |支持绿色版
|wamp|PhpStudy|https://www.xp.cn |无
|Baota|宝塔运维|https://bt.cn|无
|**IDE**|HBuilderX|https://www.dcloud.io/hbuilderx.html | 支持vue\md\html等
|IDE-JAVA|IDEA|https://www.jetbrains.com |无
|IDE-PHP|phpstorm|https://www.jetbrains.com|无
|**GUI-Redis**|RedisInsight|[ClickHere](https://redis.io/docs/stack/insight/)|可视化管理工具
|GUI-Mysql|Navicat|[ClickHere](https://navicat.com.cn/products)|可视化管理工具
|GUI-Elasticsearch|kibana|https://www.elastic.co/cn/kibana |可视化管理工具

## 其他-教程中心
|知识|教程入口|
|----|----|
|Github|https://www.bilibili.com/video/BV19b4y1p72S |
|GithubM|https://backlog.com/git-tutorial/cn |
|Redis|https://www.bilibili.com/video/BV1Dh411D7cW |
|Laravel|https://www.bilibili.com/video/BV1V4411h7JE |
|Mybaits|https://www.bilibili.com/video/BV12R4y157Be |
|ElasticSearch|https://www.bilibili.com/video/BV1Gh411j7d6 
