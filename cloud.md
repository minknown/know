
## 产品列表

| 产品类型   | aws        | aliyun | tencentyun | Aure |
|--------|------------|--------|------------|------|
| 虚拟主机   | 暂无       | 虚拟主机   | 暂无         | 暂无   |
| VPS服务器 | 暂无       | 暂无   | 暂无         | 暂无   | 
| 独立服务器  | ECS        | EC3    | 暂无         | 暂无   |
| 数据服务器  | RDS        | RDS    | 暂无         | 暂无   |
| 储存服务器  | S3         | OOS    | 暂无         | 暂无   |
| 方法服务器  | Lamada     | 函数计算   | 暂无         | 暂无   |
| 内容分发   | CloudFront | CDN    | 暂无         | 暂无   |
| 负载均衡   | LBS        | LBS    | 暂无         | 暂无   |

## 更多包括但不限制于：

1. 防火墙、Doss防护产品
2. 全文检索、搜索引擎
3. Hadoop、ks8
4. 数据流处理
5. API网关
6. 成本和预算控制
7. 5G物联网
8. 数学计算
9. 机器学习
10. 批处理
11. 量子运算
12. 域名注册

## 入口
https://aws.amazon.com/  
https://cn.aliyun.com/

## SpringCloud

>boot和cloud的版本兼容很有讲究,详见下边的链接：
> https://blog.csdn.net/mo_sss/article/details/130950161  
> **Feign远程调用出现[dispatcherServlet]错误时请考虑是否static导致的。static定的方法不会被AOP增强。**

三大微服务:Dubbo、SpringCloud(建议学习)、SpringCloudAlibaba
![](mainjs\cloud-three.jpg)

(1)引入springcloud:
````java
//或者您可以使用IDEA新建Springboot项目勾选Cloud组件。 
<properties>
        <java.version>17</java.version>
        <spring-cloud.version>2022.0.4</spring-cloud.version>
        </properties>
 <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter</artifactId>
        </dependency>
 <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
````
### (1)服务注册中心 
引入包后在启动类顶部加入@EnableEurekaServer
````java
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
````
最后配置yml:
````java
server.port=10086
spring.application.name=ser
eureka.client.service-url.defaultZone=http://127.0.0.01:10086/eureka/
````
### 服务注册
同服务注册中心一样，只需要把包‘server’改为clinet即可。无需加入@EnableEurekaServer

### 服务调用
使用Feign调用技术  
引用包后启动类顶部加入@EnableFeignClients
````java
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
````
创建一个接口，并自动状态后调用接口内对应的方法即可，注意此处和被调用的远程接口一致，无论是参数还是请求方式还是返回。
````java
@FeignClient("user")
public interface UserClient {
    @GetMapping("/user")
    String getuser();
}
````

### 服务网关：
暂无

### 拓展：
负载均衡、消息日志编码等问题、跨域、断言过滤器、集群等问题、RestTemplate(传统)\Dubbo调用法
教程来自：
>【黑马SpringCloud微服务全通关，一套精通springcloud全技术栈Eureka、 Nacos、OpenFeign、网关Gateway、 Spring-哔哩哔哩】 https://b23.tv/s9hbr90
