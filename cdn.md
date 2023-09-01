## CDN的选择
### 所有均有全球节点。

1. 国内少数被封
CF（仅移动）  
cft  

3. 畅通
bunny 
HOSTRY  
阿里云CDN  

````
CF配置踩坑指南：
DNS转移+CNAME解析即可生效。
坑比较少
````

````
Bunny配置踩坑指南：
将域名DNS转义至Bunny，建议只做wwww模式。
其中增加解析记录非www的，通过cname，转入www模式
其中增加解析记录为wwww，直接解析至目标服务器IP。
清空所有CDN列表，在DNS解析记录中直接开启所有解析条目的CDN。会自动生成所有CDN条目
如遇到HTTPS异常，检查所有CDN条目的HTTPS模式即可（无需做CNAME了即可通过HTTPS验证）。
另外还支持仅URL-CDN和WP模式
绑定账户：myjasan-email
````

````
阿里云CDN的坑比较多，特别关于回溯问题。
````

> HOSTRY 绑定账户83818278-email
> 被封不可用列表：gcore国内无法使用