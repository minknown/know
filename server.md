# server.md

## 要点
1. Iaas\Paas\Saas:I代之基础设备,P代表平台,S代表软件  
2. ERP\ORM\OA:ERP管理物料，ORM管理客户，OA管理内部的人和人活动。

   
## tomcat

````
将应用部署到根目录
方法一：（最简单直接的方法）
删除原 webapps/ROOT 目录下的所有文件，将应用下的所有文件和文件夹复制到ROOT文件夹下。
方法二：
删除原 webapps/ROOT 目录下的所有文件，修改文件“conf/server.xml”，在Host节点下增加如下Context的内容配置：
<Host name="localhost"  appBase="webapps" unpackWARs="true" autoDeploy="true"
    xmlValidation="false" xmlNamespaceAware="false">
    ......
    <Context path="" docBase="C:/apache-tomcat-6.0.32/myapps/bc.war"></Context>
</Host>
> 来自：https://blog.51cto.com/u_3871599/6283141
````

## nginx
负载均衡  

## apache

## jboss
