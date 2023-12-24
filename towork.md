#towork

+ IDEA：IDEA安装、插件、Maven源更换、项目结构，注释，文档，命名规范：见idea.md：需要根据流程操作一遍.
  
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
  见https://www.hutool.cn/的参考文档
  
  1.时间戳
  
  ````java
  System.out.println(System.currentTimeMillis());//毫秒级13位
	System.out.println(new Date().getTime());//毫秒级13位
	int x=(int)(System.currentTimeMillis()/1000);//没有毫秒级10位
  System.out.println(x);
  ````
  2.转化
  String.valueOf()一般转化为文本，或者Long.valueOf将其他转为Long，其他元素集合SET对象LIST转化再讨论。    
  3.序列化

  ````java
  //从一个对象数组字符串->对象：
    JSONArray jsonArray=JSONUtil.parseArray(html);
    int all=jsonArray.size();
    for (Object temp:jsonArray){  
        JSONObject rep = (JSONObject)temp;//rep代表当前仓库的实例。
        String name=rep.getStr("name");
     }
   //从一个对象字符串->对象：
   JSONObject rep_gitee=JSONUtil.parseObj(html);
    String name=rep_gitee.getStr("name");
  //对象、JSON、集合转为字符串
  String txt=JSONUtil.toJsonStr(obj or list);
  //转为bean:略见文档
  
  ````

  
+ 微服务
  
+ 其他：REDIS\WEB\Spring\系统