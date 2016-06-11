# ace-voip
**作者：Sipera VIPER Lab**

**License: GPLv3**
### 简介
ACE(Automated Corporate Enumerator)(自动化穷举工具）是一个简单但是很强大的工具，它可以模拟一个IP电话来得到目标IP电话的主人的姓名以及一些其他的信息。而VOIP的`"Corporate Directory"`特性可以让VOIP终端用户通过姓名直接呼叫到其VOIP手机。ACE这个工具就是让攻击者可以穷举列出`"Corporate Directory"`，这样进行攻击的时候就不仅仅是面对任意的IP地址或者一个声音片段了，而是知道了这个人的名字！ACE可以通过DHCP协议、TFTP协议、HTTP协议进行工作（下载 `VOIP Corporate Directory`),并输出为一个文本文档

### 源码

http://ucsniff.sourceforge.net/ace.html
[ace-voip项目主页](http://ucsniff.sourceforge.net/ace.html)

[kali ace-voip Repo](http://git.kali.org/gitweb/?p=packages/ace-voip.git;a=summary)

### ace-voip中包含的工具
* ace 

```shell
root@kali:~# ace
ACE v1.10: Automated Corporate (Data) Enumerator
Usage: ace [-i interface] [ -m mac address ] [ -t tftp server ip address | -c cdp mode | -v voice vlan id | -r vlan interface | -d verbose mode ]

-i (Mandatory) Interface for sniffing/sending packets
-m (Mandatory) MAC address of the victim IP phone
-t (Optional) tftp server ip address
-c (Optional) 0 CDP sniff mode, 1 CDP spoof mode
-v (Optional) Enter the voice vlan ID
-r (Optional) Removes the VLAN interface
-d (Optional) Verbose | debug mode

Example Usages:
Usage requires MAC Address of IP Phone supplied with -m option
Usage: ace -t -m

Mode to automatically discover TFTP Server IP via DHCP Option 150 (-m)
Example: ace -i eth0 -m 00:1E:F7:28:9C:8e

Mode to specify IP Address of TFTP Server
Example: ace -i eth0 -t 192.168.10.150 -m 00:1E:F7:28:9C:8e

Mode to specify the Voice VLAN ID
Example: ace -i eth0 -v 96 -m 00:1E:F7:28:9C:8E

Verbose mode
Example: ace -i eth0 -v 96 -m 00:1E:F7:28:9C:8E -d

Mode to remove vlan interface
Example: ace -r eth0.96

Mode to auto-discover voice vlan ID in the listening mode for CDP
Example: ace -i eth0 -c 0 -m 00:1E:F7:28:9C:8E

Mode to auto-discover voice vlan ID in the spoofing mode for CDP
Example: ace -i eth0 -c 1 -m 00:1E:F7:28:9C:8E
```
