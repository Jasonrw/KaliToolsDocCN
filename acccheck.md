# acccheck

**作者 ：Faisal Dean**

**License ：GPLv2**
### 简介

该工具基于SMB协议用来暴力破解Windows，它是根据`smbClient`这个二进制文件来构造的一小段代码，所以只对运行有`smbClient`这个文件的计算机终端上才有用
#### 源码
https://labs.portcullis.co.uk/tools/acccheck/

[项目主页](http://labs.portcullis.co.uk/application/acccheck)

[项目在kali上的分支](http://git.kali.org/gitweb/?p=packages/acccheck.git;a=summary)

### 项目中包含的工具
* acccheck

```bash
root@kali:~# acccheck

acccheck v0.2.1 - By Faiz

Description:
Attempts to connect to the IPC$ and ADMIN$ shares depending on which flags have been chosen, and tries a combination of usernames and passwords in the hope to identifythe password to a given account via a dictionary password guessing attack.

Usage = ./acccheck [optional]

-t [single host IP address]
OR
-T [file containing target ip address(es)]

Optional:
-p [single password]
-P [file containing passwords]
-u [single user]
-U [file containing usernames]
-v [verbose mode]

Examples
Attempt the 'Administrator' account with a [BLANK] password.
acccheck -t 10.10.10.1
Attempt all passwords in 'password.txt' against the 'Administrator' account.
acccheck -t 10.10.10.1 -P password.txt
Attempt all password in 'password.txt' against all users in 'users.txt'.
acccehck -t 10.10.10.1 -U users.txt -P password.txt
Attempt a single password against a single user.
acccheck -t 10.10.10.1 -u administrator -p password
```
### 范例
```bash
root@kali:~# acccheck.pl -T smb-ips.txt -v
Host:192.168.1.201, Username:Administrator, Password:BLANK
```
