
## 如何切换程序JDK版本
1. pom.xml中修改。
2. 项目结构中修改(位于Modules、包括level)。
3. JAVA-COMPILER修改版本。

## IDEA配置
**配置文件：在谷歌网盘下的down目录下setting.zip包**
1. 隐藏无关文件：file Type
2. 开启自动导包：Auto Import，
3. File and code：设置模板和文件注释头
4. 启动热部署：https://blog.csdn.net/m0_45877477/article/details/125446775
5. 是否界面中文，Chinese,图标为汉
   安装其他插件:  
      Code Screenshots:代码截图  
      Translation:中英翻译  
      Statistic:代码统计  
      github coplilot和Xaicoder：智能代码提示（后者为国人开发简单安装）
      mybaits log free：mybaits语句直接显示服务
6. 配置调试热键(调试或运行)
7. 配置远程主机SSH\Git\SQL等(在打开项目后)
8. 删除SpringBoot的非必要日志:新建logback.xml,留下一个空的configuration节点,关闭:
 ````
spring.main.banner-mode=off  
mybatis-plus.global-config.banner=false
 ````

## IDEA快捷键
Shift+Ctrl+/：注释，/**快速文档方法注释  
Ctrl + F9：构建/编译类  
其他没什么比较特别的，注意键位可以在IDEA设置中自定义。  

## 项目结构
MVC\MSC *(M即模型Dao,里面包括mapper和pojo,Utils建议写入Ctrl控制包中，Java视图类写在static、templates下,控制层的只是负责转发，Service层才是对某项服务功能的逻辑业务代码块。)*

## 依赖加载卡住（修改maven镜像即可）
maven的setting.xml 一般都会说在C:\Users\xxx\.m2\ 下，其实这个目录下没有，而是在idea安装目录下的插件目录下的maven目录下，如：  
C:\Program Files (x86)\JetBrains\IntelliJ IDEA 14.1.1\plugins\maven\lib\maven3\conf  
但是貌似如果.m2目录有这个文件，配置同样有用。  
最快速的简洁的方法是，右键pom.xml文件，maven-creat setting.xml即可打开或创建该文件。  
阿里云镜像的setting.xml:  
````xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
<mirrors>
    <mirror>
        <id>aliyunmaven</id>
        <mirrorOf>*</mirrorOf>
        <name>阿里云公共仓库</name>
        <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
</mirrors>
</settings>
````
