####openwrt主要功能  
- 网络功能 
- 系统管理功能  
- 状态监控功能  
***  
在openwrt固件中，几乎所有的东西都是软件包(package)，可以编译为.ipk结尾的安装包，这样就可以很方便的安装、升级和卸载。  
***  
####典型路由器应该具备以下功能  
- 支持PPPE,固定IP上网  
- DHCP动态主机配置协议 
- 网络地址转换(NAT)技术  
- 根据TCP，UDP的端口号，IP的协议号，对IP地址进行简单过滤的防火墙  
- 虚拟服务主机/端口映射(porting forwarding)技术  
- 支持一定数量的特殊应用程序 

***  
###feeds 

我们下载的openwrt源码是较为纯净的系统，feeds提供了我们在编译固件时所需的许多额外扩展软件。 

***  
###buildroot  
buildroot是一个包含Makefile和修补程序(patch)的集合，这个集合可以使你很容易的为你的目标构建交叉工具链，根文件系统以及Linux内核映像。buildroot可以独立的实现其中的一个或几个功能。   
***  
编译openwrt时出现error而终止，比如提示找不到evp.h文件而终止编译，对于Ubuntu可以使用apt-file工具，安装sudo apt-get isntall apt-file，安装成功后用apt-file update来更新源信息，然后apt-file search evp.h   
***  
###编译openwrt定制固件 
1. 用imagebuilder编译，用于灵活选择package。  
2. 用SDK编译，用于编译package仓库中没有的软件包  
3. 从源码编译，因为要重新编译cross-compile toolchains，下载内核和软件包的源码编译，导致这个过程比较耗时，用于上述两种情况搞不定的情况  
   


