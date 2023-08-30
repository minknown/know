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

### 环境建设
1.建议安装JAVA（尾部加-devel才代表JDK）
java8:sudo yum install -y java-1.8.0-openjdk*-devel
java18:sudo yum install java-17-openjdk*-devel
通过java -version验证安装，通过find / -name 'java'查找位置。  
关于java的卸载:详细见javadel.md  

2.maven的安装
maven:https://gitlab.cn/install/  
maven安装可以使用jenkins中的设置，自动安装。  
或者进入maven下载tar包进行解压后移动即可。  
测试maven可用运行绝对路径\mvn -v即可。  
需要在jenkins中设置maven路径。

3.安装git
yum install -y git即可，测试git -v

4.gitlab的安装
遵循官网步骤即可：https://gitlab.cn/install/
配置端口：ect/gitlab/rb配置文件中nignx['listen_port']、ssh_port、以及路径EXTERNAL_URL尾部增加。
配置端口注意：https需要配置复杂的SSL证书，如果是域名模式，则本地需要system32/etc/host做映射。IP的话直接以及路径EXTERNAL_URL尾部增加填写http://ip即可。
两个命令：gitlab-ctl reconfigure和gitlab-ctl restart
注意防火墙可能会导致gitlab网页无法访问。可以关闭防火墙。
gitlab中502错误、500错误、获取文件夹错误，执行reconfigure和restart一般可以修复，和内存也有一定关系。

5.jenkins的安装


