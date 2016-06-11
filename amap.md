# Amap
**作者：van Hauser and DJ RevMoon**

**License: Other**

### 简介
Amap是第一个用于渗透测试的“下一代”扫描器，主要用于软件不在其常用的端口运行的情况，甚至它可以用于不基于“ASCII”开发的软件。它的工作原理主要是发送软件的触发包（Trigger Packets），然后根据端口的返回包确定软件和软件版本。

### 源码
[Amap 主页](http://www.thc.org/thc-amap/)

[Kali 项目主页](http://git.kali.org/gitweb/?p=packages/amap.git;a=summary)

### Amap中包含的工具

* amapcrap - 向UDP、TCP、SSL端口发送一段随机的数据并确认其返回值

```shell
root@kali:~# amapcrap
amapcrap v5.4 (c) 2011 by van Hauser/THC &lt;vh@thc.org&gt;

Syntax: amapcrap [-S] [-u] [-m 0ab] [-M min,max] [-n connects] [-N delay] [-w delay] [-e] [-v] TARGET PORT

Options:
-S use SSL after TCP connect (not usuable with -u)
-u use UDP protocol (default: TCP) (not usable with -c)
-n connects maximum number of connects (default: unlimited)
-N delay delay between connects in ms (default: 0)
-w delay delay before closing the port (default: 250)
-e do NOT stop when a response was made by the server
-v verbose mode
-m 0ab send as random crap:0-nullbytes, a-letters+spaces, b-binary
-M min,max minimum and maximum length of random crap
TARGET PORT target (ip or dns) and port to send random crap

This tool sends random data to a silent port to illicit a response, which can
then be used within amap for future detection. It outputs proper amap
appdefs definitions. Note: by default all modes are activated (0:10%, a:40%,
b:50%). Mode 'a' always sends one line with letters and spaces which end with
\r\n. Visit our homepage at http://www.thc.org
```
* amap - 主程序：“下一代扫描器”

```bash
root@kali:~# amap
amap v5.4 (c) 2011 by van Hauser &lt;vh@thc.org&gt; www.thc.org/thc-amap
Syntax: amap [-A|-B|-P|-W] [-1buSRHUdqv] [[-m] -o ] [-D ] [-t/-T sec] [-c cons] [-C retries] [-p proto] [-i ] [target port [port] ...]
Modes:
-A Map applications: send triggers and analyse responses (default)
-B Just grab banners, do not send triggers
-P No banner or application stuff - be a (full connect) port scanner
Options:
-1 Only send triggers to a port until 1st identification. Speeeeed!
-6 Use IPv6 instead of IPv4
-b Print ascii banner of responses
-i FILE Nmap machine readable outputfile to read ports from
-u Ports specified on commandline are UDP (default is TCP)
-R Do NOT identify RPC service
-H Do NOT send application triggers marked as potentially harmful
-U Do NOT dump unrecognised responses (better for scripting)
-d Dump all responses
-v Verbose mode, use twice (or more!) for debug (not recommended :-)
-q Do not report closed ports, and do not print them as unidentified
-o FILE [-m] Write output to file FILE, -m creates machine readable output
-c CONS Amount of parallel connections to make (default 32, max 256)
-C RETRIES Number of reconnects on connect timeouts (see -T) (default 3)
-T SEC Connect timeout on connection attempts in seconds (default 5)
-t SEC Response wait timeout in seconds (default 5)
-p PROTO Only send triggers for this protocol (e.g. ftp)
TARGET PORT The target address and port(s) to scan (additional to -i)
amap is a tool to identify application protocols on target ports.
Note: this version was NOT compiled with SSL support!
Usage hint: Options "-bqv" are recommended, add "-1" for fast/rush checks.
```

### 用法示例
扫描*192.168.1.15*上的*80*端口，使用amap推荐的**-bqv**。
**b**:显示收到的内容名称
**q**:不显示关闭的端口
**v**:显示扫描详细状态和进度
```bash
root@kali:~# amap -bqv 192.168.1.15 80
Using trigger file /etc/amap/appdefs.trig ... loaded 30 triggers
Using response file /etc/amap/appdefs.resp ... loaded 346 responses
Using trigger file /etc/amap/appdefs.rpc ... loaded 450 triggers

amap v5.4 (www.thc.org/thc-amap) started at 2014-05-13 19:07:16 - APPLICATION MAPPING mode

Total amount of tasks to perform in plain connect mode: 23
Protocol on 192.168.1.15:80/tcp (by trigger ssl) matches http - banner: \n\n501 Method Not Implemented\n\n
<h1>Method Not Implemented</h1>
\n

to /index.html not supported.
\n

\n

<hr />

\n

<address>Apache/2.2.22 (Debian) Server at 12
Protocol on 192.168.1.15:80/tcp (by trigger ssl) matches http-apache-2 - banner: \n\n501 Method Not Implemented\n\n</address>
<h1>Method Not Implemented</h1>
\n

to /index.html not supported.
\n

\n

<hr />

\n

<address>Apache/2.2.22 (Debian) Server at 12
Waiting for timeout on 19 connections ...</address>amap v5.4 finished at 2014-05-13 19
```
