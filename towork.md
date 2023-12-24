#towork

+ IDEA：IDEA安装、插件、Maven源更换、项目结构，注释，文档，命名规范：见idea.md：需要根据流程操作一遍
+ MYBAIT和REASFUL：
  优先使用plus，REASFUL格式见mainjs/Rest.png
  1.在application.properties中配置mysql数据库信息（具体见config.md）。    
  2.添加一个Mapper/pojo,pojo需要@TableName(tablename),Mapper为接口且继承BaseMapper。    
  3.在启动入口@SpringBootApplication下添加MapperScan（到Mapper的目录，右键Mapper文件夹Copy包名字）。   
  4.注意mysql版本和pom中驱动版本以及SpringBoot版本问题，然后在控制类中做扫描即可。    
  5.注意：自定义语句写在Mapper中，@Select("select * from cai where id=22")public List<Cai> gethj();   
  
  ````java
        @Controller
        public class hello {
            @Autowired
            private CaiMapper aaa;//aaa爆红和ico容器有关，实际不影响运行。
            @RequestMapping("/login/{name}")
            @ResponseBody
            public String hello(@PathVariable String name){
                List<Cai> x;
                x = aaa.selectList(null);
                x.forEach(System.out::println);
                System.out.println("------------");
                System.out.println(aaa.gethj());
                return "hello,"+name;
            }
        }

  ````

+ hutools

  
+ 微服务
+ 其他：REDIS\WEB\Spring\系统
