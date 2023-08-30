## known_fusion:一个关于Vmware、gitlab、jenkins的集成项目。

### 第一步：vm虚拟机(centos)的安装
1. 组网：桥接模式(常用)：和物理机组为局域网 ; NAT模式：和外部本机电脑当作路由器
2. 组网可能可能还会遇到IP变化和网段问题，在VMware中编辑菜单-虚拟网络编辑器，选择网络模式，进行下边子网IP和子网掩码、DHCP设置。  
3. 通过ip addr查看ip.IP地址可能每次启动会重新跳动，可通过百度自行设置固定（在linux中vim配置进行设置IP固定）。
4. 建议虚拟机配置，最低8G内存+30G硬盘，外部非虚拟机的话16G+256G硬盘
5. 安装好后检查防火墙是否关闭，通过yum install wget测试yum，如有Appstem\repotity的问题请配置yum源，尤其在centos8下yum源暂停服务的情况下，确认yum正常可以使用后，sudo yum update，更新yum源。
````
cd /etc/yum.repos.d
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo
sed -i -e "s|mirrors.cloud.aliyuncs.com|mirrors.aliyun.com|g " /etc/yum.repos.d/CentOS-*
sed -i -e "s|releasever|releasever-stream|g" /etc/yum.repos.d/CentOS-*
yum clean all && yum makecache
````
### 环境建设
1.建议安装JAVA
java8:yum install -y java-1.8.0-openjdk*
通过java -version验证安装，通过find / -name 'java'查找位置。
gitlab的安装：
yum install wget测试可用。
然后按照官方的步骤直接按照即可。
安装完毕配置ect/gitlab/rb

检查内存、配置端口只需要改rb.listen_port即可。502问题、获取文件夹错误等一会刷新和内存有关即可、
 p0lW9F5SoP0+UBaRe9Utr6bvX+PPlcpA7UO7ChEFFHQ=（会被删除）
打不开管理平台网页？检查并关闭防火墙再试。


jenkins
kafaka+springcloud
