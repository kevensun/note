通常，计算机的CPU并不是直接和usb设备打交道，而是和控制器打交道。它要对设备做什么，它会告诉控制器，而不是直接把指令发给设备。然后控制器再去负责处理这件事情，它会去指挥设备执行命令，而CPU就不用管剩下的事情。控制器替他去完成剩下的事情，事情办完了在通知CPU   
现实中经常是一个usb控制器和一个hub绑定在一起，专业一点成为集成，而这个hub也被称作roothub    
usb总线是一种轮询式总线，协议规定所有的数据传输都必须由主机发起，由主机控制器初始化所有的数据传输。   
usb core从usb子系统的初始化开始，位于drivers/usb/core/usb.c  subsys_initcall()     
一个设备可以有多个接口，每个接口对应不同的驱动程序    
kobject是基类，所实现的只是一些公共接口，kset是同种类型kobject对象的集合，也可以说是对象的容器    
***  
一般来说，我们平时所谓的编写USB驱动指的也就是写USB接口的驱动，需要以一个struct usb_driver结构的对象为中心，以设备的接口提供的功能为基础，开展USB驱动的建设。   
***   
powered->default(收到复位信号)->address(hub使用core中定义的一个函数usb_control_msg给设备发送SET_ADDRESS请求)   
***   
控制传输三阶段：SETUP/DATA/STATUS   
usb_internal_msg调用usb_internal_usb_control_msg包含usb_alloc_urb/usb_fill_control_urb/usb_start_wait_urb