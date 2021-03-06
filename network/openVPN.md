
#### /etc/openvpn/server.conf
```js
root@:/etc/openvpn# cat server.conf
port 1194
proto tcp
dev tun
sndbuf 0
rcvbuf 0
ca ca.crt
cert server.crt
key server.key
dh dh.pem
auth SHA512
tls-auth ta.key 0
topology subnet
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS 114.114.114.114"
push "dhcp-option DNS 192.168.66.1"
push "route 192.168.64.0 255.255.255.0"
push "route 192.168.65.0 255.255.255.0"
push "route 192.168.66.0 255.255.255.0"
push "route 118.26.172.0 255.255.255.0"
client-to-client
duplicate-cn
keepalive 10 120
;comp-lzo
max-clients 1000
cipher AES-256-CBC
user nobody
group nogroup
persist-key
persist-tun
status openvpn-status.log
verb 3
crl-verify crl.pem
root@:/etc/openvpn# 
```

### 最简单安装 openVPN
* http://netsecurity.51cto.com/art/201704/537925.htm

* https://raw.githubusercontent.com/Nyr/openvpn-install/master/openvpn-install.sh
* https://blog.csdn.net/l1028386804/article/details/72190429
* https://blog.csdn.net/huihui1094667985/article/details/79507044

### 下载 openvpn-install.sh 并执行，第一个IP是 server端坚听的IP 公网IP
* https://github.com/Nyr/openvpn-install

```
 1001  cd github/
 1005  wget https://raw.githubusercontent.com/Nyr/openvpn-install/master/openvpn-install.sh
 1007  chmod +x *.sh
 1015  chmod +x *.sh.1
 1017  ./openvpn-install.sh.1
 1018  cd /root
 1019  ll client.ovpn 
 1022  ps -ef | grep vpn
 1024  cd /etc/openvpn
 1026  vi server.conf
 1027  ps -ef | grep vpn
 1028  netstat -lntp
 1029  netstat -lntpa

 1032  cp client.ovpn  /tmp
 1033  chmod +r /tmp/client.ovpn 
 1035  ps -ef | grep vpn
 1037  netstat -lntpa
 1038  arp -a
 1039  ip add 
 1040  ping 10.8.0.2
 1041  ip route
```
### 主机上的配置
```
15: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 100
    link/none 
    inet 10.8.0.1/24 scope global tun0
       valid_lft forever preferred_lft forever
    inet6 fe80::b330:adef:86a8:6266/64 scope link stable-privacy 
       valid_lft forever preferred_lft forever
lgf@develop:~$ 
```
如果主机上看到的 tun0处于DOWN的状态，执行以下命令
```
# ip link set tun0 up
# ip addr add 10.8.0.1/24 dev tun0
```
参考如下：
* https://backreference.org/2010/03/26/tuntap-interface-tutorial/
```
# openvpn --mktun --dev tun2
Fri Mar 26 10:29:29 2010 TUN/TAP device tun2 opened
Fri Mar 26 10:29:29 2010 Persist state set to: ON
# ip link set tun2 up
# ip addr add 10.0.0.1/24 dev tun2
```

### 开关机shell
```
root@henrongyi:/usr/bin# ll open*.sh
-rwxr-xr-x 1 root root 321 Sep 13 01:12 openvpn-ctl.sh
root@henrongyi:/usr/bin# 
root@henrongyi:/usr/bin# cat open*.sh
case "$1" in
start)
    systemctl start openvpn@server.service
    sleep 2
    #ip link set tun0 up
    #ip addr add 10.8.0.1/24 dev tun0
;;
stop)
    systemctl stop openvpn@server.service
;;
*)
   echo "Usage: $0 {start|stop|reload|restart|force-reload|cond-restart|soft-restart|status}" >&2
   exit 1
   ;;
esac
exit 0
root@henrongyi:/usr/bin# 
```

### 主机上还要配置路由
配置一条默认路由
```
root@develop:/usr/bin# 
root@develop:/usr/bin# ip route
default via 192.168.66.1 dev enp11s0f0 
default via 192.168.66.1 dev enp11s0f0 proto static 
10.8.0.0/24 dev tun0 proto kernel scope link src 10.8.0.1 
192.168.66.0/24 dev enp11s0f0 proto kernel scope link src 192.168.66.253 
root@develop:/usr/bin# 
root@develop:/usr/bin# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         192.168.66.1    0.0.0.0         UG    0      0        0 enp11s0f0
0.0.0.0         192.168.66.1    0.0.0.0         UG    0      0        0 enp11s0f0
10.8.0.0        0.0.0.0         255.255.255.0   U     0      0        0 tun0
192.168.66.0    0.0.0.0         255.255.255.0   U     0      0        0 enp11s0f0
root@develop:/usr/bin# 
```

*  https://blog.csdn.net/yuanchao99/article/details/18992567

### windows client
2.下载客户端
MAC：
https://www.tunnelblick.net/downloads.html

WindowOS（64bit）：
http://swupdate.openvpn.org/community/releases/openvpn-install-2.3.3-I002-x86_64.exe
WindowOS（32bit）
http://swupdate.openvpn.org/community/releases/openvpn-install-2.3.3-I002-i686.exe


* https://www.cnblogs.com/EasonJim/p/8341404.html
* https://blog.csdn.net/huihui1094667985/article/details/79507044
* https://openvpn.net/release/ 下载 openvpn-2.1.3-install.exe	21-Feb-2012 00:50	1.6M

再次运行openvpn-install.sh 可以生成不同的 .opvn 文件。

将 /tmp/client.ovpn 这个文件复制出来，放在 C:\Program Files (x86)\OpenVPN\config 这个目录下。
然后在window上运行 OpenVPN GUI 这个client，点connect即可。

再次运行openvpn-install.sh 可以生成不同的 .opvn 文件。

### 其它信息

【51CTO.com快译】本文介绍了如何在基于RPM和DEB的系统中安装和配置OpenVPN服务器。我们在本文中将使用一个名为openvpn-install的脚本，它使整个OpenVPN服务器的安装和配置过程实现了自动化。该脚本可帮助你在几分钟内搭建好自己的VPN服务器，哪怕你之前没有用过OpenVPN。

好了，闲话少说。

在Linux中安装和配置OpenVPN Server

出于本文的需要，我将使用两个运行CentOS 7 64位版本的系统。一个充当OpenVPN服务器，另一个充当OpenVPN客户机。下面是测试系统的详细信息。

OpenVPN服务器：
操作系统：CentOS 7 64位极简版
IP地址：192.168.43.150/24
主机名称：vpnserver.ostechnix.local
OpenVPN客户机：
操作系统：CentOS 7 64位极简版
IP地址：192.168.43.199/24
我们先来看看服务器端配置。

OpenVPN Server的安装和配置

从GitHub页面下载openvpn-install脚本。

wget https://git.io/vpn -O openvpn-install.sh

然后，使用下列命令，以root用户的身份运行该脚本：

bash openvpn-install.sh 
系统会要求你回答一系列问题。回答相应的问题。

确保VPN服务器的IP地址正确。如果你使用多个IP地址，输入想让OpenVPN侦听的那个网络接口的IP地址。

Welcome to this quick OpenVPN "road warrior" installer
I need to ask you a few questions before starting the setup
You can leave the default options and just press enter if you are ok with them
First I need to know the IPv4 address of the network interface you want OpenVPN
listening to.
IP address: 192.168.43.150
选择你想使用哪种协议。我想要使用tcp端口，因此选择了数字2。

Which protocol do you want for OpenVPN connections?

1) UDP (recommended)

2) TCP

Protocol [1-2]: 2

输入端口号。

What port do you want OpenVPN listening to?

Port: 1194

输入你想与VPN结合使用的DNS服务器细节。我想使用谷歌DNS解析器，于是选择了选项2。

Which DNS do you want to use with the VPN?

1) Current system resolvers

2) Google

3) OpenDNS

4) NTT

5) Hurricane Electric

6) Verisign

DNS [1-6]: 2

我们已到了最后一步。输入你的客户机证书名称。这个名称应该是一个单词，不该含有任何特殊字符。

Finally, tell me your name for the client certificate
Please, use one word only, no special characters
Client name: client
按回车键，开始OpenVPN服务器的安装。

Okay, that was all I needed. We are ready to setup your OpenVPN server now
Press any key to continue...
没有任何问题，该脚本会开始装上安装OpenVPN服务器需要的所有必要依赖项。另外，它还会创建所有必要的密钥和证书，以便通过VPN客户机的验证。这个过程需要几分钟。

最后，脚本会问你有没有任何外部IP地址。如果没有外部IP地址，就让它空着，不用管，按回车键。

If your server is NATed (e.g. LowEndSpirit), I need to know the external IP
If that's not the case, just ignore this and leave the next field blank
External IP:
Finished!
Your client configuration is available at /root/client.ovpn
If you want to add more clients, you simply need to run this script again!
OpenVPN服务器的安装和配置已完成。你从最后的输出中可以看出，客户机配置细节保存在文件/root/client.ovpn中。需要将该文件拷贝到你的所有VPN客户机系统。

我将client.ovpn文件拷贝到了我的VPN客户机。

scp client.ovpn root@192.168.43.199:/etc/openvpn/ 
接下来，我们需要配置OpenVPN客户机。

OpenVPN客户机的配置

确保你从VPN服务器系统拷贝过来了client.ovpn文件。我已经将这个文件拷贝到VPN客户机系统的/etc/openvpn/目录。
