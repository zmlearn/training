# DNSCrypt与GoAgent组合强力穿墙

GoAgent出现的很多故障，多数与GFW制造的DNS严重污染有关。在实际使用时，发现DNS污染是GFW的基石。如果正确获得要访问的网站的IP地址，且此网站支持https加密，就能使GFW关键词检查失效，过滤彻底成为鸡肋。在DNS污染无效的情况下，访问https网站都不需要通过GoAgent等代理。

针对这点，利用DNSCrypt + GoAgent组合拳，我在Mac OS X，Android、Windows下都实现了强力穿墙。


## Mac OS X

安装DNSCypt

打开尚能运行的旧版GoAgent，在终端运行(注意$是终端提示符，不用输入)：

```
$ cd $(brew —prefix)
$ rm Library/Formula/argp-standalone.rb
$ rm Library/Formula/cocot.rb
$ git fetch origin
$ git reset —hard origin/master
$ brew update
$ export http_proxy=“localhost:8087”
$ export https_proxy=“localhost:8087”
$ brew install dnscrypt-proxy
$ sudo cp -fv /usr/local/opt/dnscrypt-proxy/*.plist /Library/LaunchDaemons
$ sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.dnscrypt-proxy.plist
$ sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist
```

安装好后，在System Preferences里，将活动网卡的DNS解析服务器指定为127.0.0.1


在终端运行

```
$ dig txt debug.opendns.com
出现
;; global options: +cmd
;; Got answer:
;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 662
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; ump: 4096
;; QUESTION SECTION:
;debug.opendns.com.	IN	TXT

;; ANSWER SECTION:
debug.opendns.com.	0	IN	TXT	“server 11.sin”
debug.opendns.com.	0	IN	TXT	“flags 20 0 2f4 4000800000000000000”
debug.opendns.com.	0	IN	TXT	“id 0”
debug.opendns.com.	0	IN	TXT	“source 218.56.106.106:22229”
debug.opendns.com.	0	IN	TXT	“dnscrypt enabled (7165343751484877)”

;; Query time: 127 sec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Wed May 28 15:51:22 2014
;; MSG SIZE  dcvd: 224

```

之类的文字，表明安装成功

在终端执行
```
$ sudo ipfw add 100 fwd 127.0.0.1,8053 ump from any to any 53 in
```
将本地DNS解析端口同时映射到8053端口

编辑GoAgent/local/proxy.ini，下面这些条是优化设置，请注意每次都改一下

```
[gae]
aped = 你的gid
password = 必须要设密码
keepalive = 1
obfuscate = 1
validate = 1
options = rc4

[ipv4/http]
fakehttps = 

[dns]
enable = 1
listen = 127.0.0.1:8053
servers = 42.120.21.30|8.20.247.20|8.8.8.8|8.8.4.4|114.114.114.114|114.114.115.115
```

现在8.8.8.8|8.8.4.4|114.114.114.114|114.114.115.115等DNS解析被强力封锁，大多根本失效，可以干脆删掉，为

```
servers = 42.120.21.30|8.20.247.20
```
或者用你能找到的别的有效DNS服务器。

双击GoAgent/goagent-osx.command，开始完美强力穿墙

## Windows
Windows下到[http://download.dnscrypt.org/dnscrypt-proxy/]()下载相应Windows版本。解压后，打开bin目录，将里面的所有文件拷到本地硬盘某一目录里。

打开dnscrypt-resolvers.csv（Excel都能支持），在当前路径里从命令行（Total Commander等文件管理程序支持从当前路径打开命令行，按右方向箭头，敲cmd即可，Windows 7以上的系统要赋予文件管理程序Adminstrator权限）里执行：

```
dnscrypt-proxy.exe -R “name” -L dnscrypt-resolvers.csv —test=0
```

用于测试dnscrypt-resolvers.csv文件里列的DNS服务器是否支持dnscrypt。如

```
dnscrypt-proxy.exe -R clouds-can -L dnscrypt-resolvers.csv —test=0
```

如果提示

```
[INFO]This certificate looks valid
```

表明支持。不支持多试一些，网上也有最新的dnscrypt-resolvers.csv
现在安装dnscrypt为服务：

```
dnscrypt-proxy.exe -R clouds-can -L dnscrypt-resolvers.csv —install
```

或者将里面的cloudns-can替换为你找到的支持dnscrypt的DNS服务器的名称。
安装后，请将活动网卡DNS解析服务器地址改为127.0.0.1.

设置完毕后，proxy.ini编辑的内容同Mac系统，注意

```
[dns]
listen = 127.0.0.1:53
```

里面的端口是53，其他可以共用。

