# NoClassDefFound.md
## 曾经在niceoauto项目的错误异常经验NoClassDefFound
一方面是目录错乱导致  
另一方是lib包，Project-Structure中Artifacts中添加EXTRACTED-DIR  
C:\Users\Administrator\.m2\repository\commons-net\commons-net\3.9.0\commons-net-3.9.0.jar（每个场景不同）  
即可   
>你这套不是完全基于maven构建的 maven在你这个项目里就充当了下载的功能 构建是依赖于idea的 
如果你构建也是让maven来搞就没这个问题了
