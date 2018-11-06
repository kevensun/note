在.dts文件的每个设备，都有一个compitible属性，compatible属性用于驱动和设备的绑定。 compatible属性是一个字符串的列表，列表中的第一个字符表征了节点代表的确切设备，形式为“manufacture，model”，其后的字符串表征可兼容的其他设备。可以说前面的是特指，后面的则涵盖更广的范围。 
***  

address和length字段是可变长的，父节点的#address-cells和#size-cells分别决定了子节点的reg属性的address和length字段的长度  
***    

设备树是从软件使用的角度描述硬件的，不是从硬件设计的角度描述的。对于软件可以自动识别的硬件，如USB设备，PCI设备，也是没有必要通过设备树描述的。