## known_fusion:一个关于Vmware、gitlab、jenkins的集成项目。

### 第一步：centos以及vm的安装
1. 组网：桥接模式(常用)：和物理机组为局域网 ; NAT模式：和外部本机电脑当作路由器
2. 组网可能可能还会遇到IP变化和网段问题，在VMware中编辑菜单-虚拟网络编辑器，选择网络模式，进行下边子网IP和子网掩码、DHCP设置。  
3. 通过ip addr查看ip.IP地址可能每次启动会重新跳动，可通过百度自行设置固定（在linux中vim配置进行设置IP固定）。
4. 建议虚拟机配置，最低8G内存+30G硬盘，外部非虚拟机的话16G+256G硬盘
5. 安装好后检查防火墙是否关闭，通过yum install wget测试yum，如有Appstem\repotity的问题请配置yum源，尤其在centos8下yum源暂停服务的情况下:  
````
cd /etc/yum.repos.d
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
sed -i -e "s|mirrors.cloud.aliyuncs.com|mirrors.aliyun.com|g " /etc/yum.repos.d/CentOS-*
sed -i -e "s|releasever|releasever-stream|g" /etc/yum.repos.d/CentOS-*
yum clean all && yum makecache
````
6.确认yum正常可以使用后，sudo yum update，更新yum源。

### 第二步：JAVA环境建设
Jenkins需要jdk\git\maven才能基本型地运行。  
所以可通过下边安装JAVA（尾部加-devel才代表JDK）
````
java8:sudo yum install -y java-1.8.0-openjdk*-devel
java18:sudo yum install java-17-openjdk*-devel
````
> 通过java -version验证安装。  
> 通过find / -name 'java'、which java、whereis java查找jdk安装的位置。  
> 通过yum search java | grep java 搜索java的所有软件包。  
> 关于java的卸载:详细见本博客的：javadel.md。  

### 第三步：maven的安装
maven官网:[https://gitlab.cn/install/  ](https://maven.apache.org/download.cgi)  
maven安装可以使用jenkins中的设置，自动安装。  
或者进入maven下载tar.gz包进行解压后移动mv即可(推荐移动至/usr/local/maven下)。  
测试maven可用运行绝对路径\mvn -v即可，即/usr/local/maven/mvn -v。  
注意：需要在jenkins中设置maven路径。  

### 第四步：安装git
yum install -y git即可，测试git -v

### 第五步：gitlab的安装

安装过程：遵循官网步骤即可：https://gitlab.cn/install/

**端口配置：**
配置端口：ect/gitlab/rb配置文件中nignx['listen_port']、ssh_port、以及路径EXTERNAL_URL尾部增加。  
配置端口注意：  
1. https需要配置复杂的SSL证书，如果是域名模式，则本地需要system32/etc/host做映射。
2. IP的话直接以及路径EXTERNAL_URL尾部增加填写http://ip即可。  
**两个命令：gitlab-ctl reconfigure和gitlab-ctl restart**

**用户验证：**
````
SSH生成:ssh-keygen -t rsa -C "xxxxx@xxxxx.com"  
SSH位置:c:/user/.ssh/或 ~/.ssh/id_rsa.pub（linux）  
git config --global user.name "username" //（名字）  
git config --global user.email "username@email.com" //(注册账号时用的邮箱)   
git config --list //查看配置是否存在和内容。    
````

**常见报错：** 
1. 平台网页无法打开:注意防火墙可能会导致gitlab网页无法访问。可以关闭防火墙再试。    
2. gitlab中502错误、500错误、获取文件夹错误：执行reconfigure和restart一般可以修复，和内存也有一定关系。    
3. gitlab ! [remote rejected] master -> master (pre-receive hook declined) error: failed to push some refs to ' :
用户没有push权限或者分支被保护。   

### 第六步：jenkins的安装
官网：https://www.jenkins.io/zh/  
下载war包，进入java -jar war即可启动jenkins。启动失败请尝试--httpPort=7777修改端口再试。  
常用插件：git-paren（参数用）maven inter（maven项目）ssh-publier(将包发送至另一个SSH用)  
通常，新建一个maven任务，设置git仓库地址，maven位置，勾选构建成功运行，即可开始一个任务。  
建议，为了增加maven构建速度，建议设置aliyun的镜像源，

### 附件：设置maven的镜像源
打开 Maven 的 settings.xml 文件：在 Maven 安装目录下的 conf 文件夹中，找到 settings.xml 文件，并打开它。  
添加镜像配置：在 settings.xml 文件中，找到 <mirrors> 元素，并添加以下配置后保存退出即可：  
````
<mirrors>
    <mirror>
        <id>aliyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Aliyun Mirror</name>
        <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
</mirrors>
````





