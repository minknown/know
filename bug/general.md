# knowForBug
存放IDEA配置、pom依赖(包括创建项目)、一些常见Bug解决和版本规定。

## BUG问题和版本兼容

````
>java: 警告: 源发行版 17 需要目标发行版 17

>6152错误(SpringBoot和JDK)
````

>这个问题是JDK和SpringBoot版本不兼容导致的 。   
>要么切换项目JDK版本，要么切换SpringBoot版本(pom-parent)。   
>SpringBoot V3.0.2 >=JDK 17;  
>SpringBoot V2.7.8/2.4.5 >=JDK 8;  
*另外一点:不同版本的IDEA所支持的JDK版本也不一样，在2020版本的IDEA当中是不支持JDK17的。*
*如果你没有使用Springboot,可以在设置中-构建-JAVA-Compier改为8版本即可解决*  

````
数据库查询不出来的错误
````

>这个问题是当前数据库版本和数据库驱动不兼容导致的。  
>mysql V5-V8 >=驱动  5.1.47;(mysql-connector-java)  
>mysql V8 >=驱动 8.0.0（jc）;   
*另外一点:mybaits也可能遇到这个情况，可以从3.0切回2.0即可解决*


````
org.apache.ibatis.binding.BindingException: Invalid bound statement (not found): com.example.sqldemo.Mapper.UserMapper
java.lang.NoClassDefFoundError: org/springframework/aot/AotDetector
A component required a bean of type ‘com.XXX.XXX.XXX‘ that could not be found
Property 'sqlSessionFactory' or 'sqlSessionTemplate' are required
````
>重复引用(mybatis-plus有了不需要再导入mybatis);
>另外也可能是SpringBoot需要从3降低到2.7.9;
>加一个scanmapper，mapper注解两个都需要;


````
Mybaits-plus遇到的问题：
java.sql.SQLNonTransientConnectionException: CLIENT_PLUGIN_AUTH is required
java.lang.IllegalArgumentException: Invalid value type for attribute 'factoryBeanObjectType': java.lang.String
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'hello':
````
>一个pom中mysql驱动版本的问题，另一个是springboot版本兼容问题，可以下调到2.7.8问题（bean类关键字的提示都可能是这个问题导致）。
