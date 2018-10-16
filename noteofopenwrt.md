##openwrt开发笔记  
###固件编译  
虚拟机：Ubuntu14.04 64位，联网，足够硬盘空间(大于60G)
选用无涯stable版本：  
1. git clone https://github.com/hi-wooya/openwrt-hiwooya-stable.git   
2. 进入openwrt源码目录，执行./scripts/feeds update –a  
3. ./scripts/feeds install –a   
4. 执行make menuconfig ，其中target system选Ralink RT288x/RT3xxx; subtarget选MT7620 base boards;target profile选HiWooya7620  
5. 执行make V=99进行编译(首次编译时间较长，请耐心等待)  
6. 若编译成功，则bin/ramips/目录下的openwrt-ramips-mt7620-HiWooya7620-squashfs-sysupgrade.bin即是编译好的固件    
*** 
###编译中可能遇到的问题  
 1. 编译过程需要下载，需要科学上网  
 2. 如果下载遇到困难，将3th_MT7620A开发套件光盘资料\配套开发所有源码\openwrt-1505-dl.tar.bz2解压，将里边所有文件拷到dl目录，重新编译

***  

###固件烧录   
1. 开发板COM连接电脑，串口工具波特率57600，上电，倒数结束前按空格，进入uboot(串口显示breed>表明成功)；  
2. 开发板任一LAN口用网线连接到电脑主机，电脑浏览器192.168.1.1进入Breed Web恢复控制台   
3. Breed Web恢复控制台左侧选择固件更新，在右侧固件位置浏览选择编译好的固件，点击上传，确认信息后点更新，等待完成重启
 
***   
###WAN口配置  
/etc/config/network为网络配置，修改config interface 'lan'中的option ipaddr ，不要跟上级网络一个网段  base-files/files/etc/config/network
###WIFI配置   
1. 在make menuconfig时取消原网卡驱动：kernel modules->wireless drivers->kmod-rt2800-soc取消勾选  
2. 选择新驱动：勾选ralink->ralink-wifi,重新编译  
###修改WiFi名与密码  
- 修改配置文件方式：/etc/config/wireless  
- 修改源码：openwrt-hiwooya-stable/package/hiwooya-wifi/ralink-wifi/files/lib/wifi/ralink.sh中从后往前看

###配置luci  
- 无涯定制：make menuconfig:utilities->luciapk  
- 原生：luci->1.collections->luci;2.luci->modules->translations->chinese