# kali无法联网
### 情况一，桥接模式下ifconfig没有eth0 接口
* ```
    # 编辑interfaces文件
    sudo vim /etc/network/interfaces
    # 若没有以下内容则新增
    auto eth0
    iface eth0 inet dhcp
* ```
    # 重启网络
    /etc/init.d/networking restart
    # 也可用
    systemctl restart networking   

* ```
    # 注销，重新进入桌面

### 情况二，有eth0，没有IP地址
* ```
    # 启用网卡
    sudo ifconfig eth0 up  
    # 分配IP
    sudo dhclient eth0  

    # 释放ip
    sudo dhclient -r eth0

### 情况三，设置了代理，真机中没有开启允许lan连接

### 常用解决方法
* `重置虚拟网络编辑器`