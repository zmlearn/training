#### 介绍

为什么要翻墙？因为 我们日常/工作中需要用到的某些网络资源来源（或网站， 在线服务）被国家的网络防火墙限制 正常访问。

比如 [google](https://google.com), [github](https://github.com), [stackoverflow](https://stackoverflow.com) …

#### 常用的翻墙手段
##### PAC(自动代理配置文件模式), APN, OpenVPN

收费服务商(他们都有对应的设置教程)

- [https://myxgj.com/](https://myxgj.com/)
- [http://www.waimaot.com/](http://www.waimaot.com/)

##### GoAgent

使用goagent的关键是要找到可用的google IP

- [goagent](https://github.com/goagent/goagent)
- [gogo tester](https://code.google.com/p/gogo-tester/)
- [DNSCrypt与GoAgent组合强力穿墙](DNSCrypt与GoAgent组合强力穿墙.md)
- [GoAgent在MacOS 中的使用](https://github.com/comeforu2012/GoAgentForMacOS/wiki)
- [XWall 集成GoAgent支持](https://github.com/lunadream/XWall)

##### ShadowSocks

shadowsocks在普通的socks代理上进行了自定义加密方式等改进，支持多个平台，迄今为止GFW还无法通过特制检测进行封杀，总的来说还是比较坚挺的，唯一的缺点就是需要自行租用VPS并部署服务器端
也有一些付费shadowsocks账号提供商，价格比起VPN来要低上很多

[科学上网利器 Shadowsocks 使用方法](http://ttt.tt/150/)

[shadowsocks介绍](https://plus.google.com/+GhostAssassin/posts/TtWFAQmSMVE)

##### SSH 代理翻墙方式

Secure Shell（缩写为SSH），由IETF的网络工作小组（Network Working Group）所制定；SSH为一项创建在应用层和传输层基础上的安全协议，为计算机上的Shell（壳层）提供安全的传输和使用环境。

传统的网络服务程序，如rsh、FTP、POP和Telnet其本质上都是不安全的；因为它们在网络上用明文传送数据、用户帐号和用户口令，很容易受到中间人（man-in-the-middle）攻击方式的攻击。就是存在另一个人或者一台机器冒充真正的服务器接收用户传给服务器的数据，然后再冒充用户把数据传给真正的服务器。

而SSH是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用SSH协议可以有效防止远程管理过程中的信息泄露问题。通过SSH可以对所有传输的数据进行加密，也能够防止DNS欺骗和IP欺骗。

SSH之另一项优点为其传输的数据可以是经过压缩的，所以可以加快传输的速度。SSH有很多功能，它既可以代替Telnet，又可以为FTP、POP、甚至为PPP提供一个安全的“通道”。

SSH本来是为网站管理员准备的，目的是让管理员可以远程进入网站服务器并修改数据的同时不让这数据被黑客截留篡改，也就是说SSH会将要传输的数据进行强加密。对，与远程服务器通信，进行强加密，也就是说可以绕过GFW的审查，这就是SSH的翻墙原理
————

收费SSH代理服务商

- [OnlyBird](http://blog.onlybird.com/%E6%94%B6%E8%B4%B9ssh%E4%BB%A3%E7%90%86)
- [tngrnow](https://tngrnow.net/price.php)

翻墙客户端

- [XWall ](https://github.com/lunadream/XWall)
- [MyEnTunnel](http://nemesis2.qx.net/pages/MyEnTunnel)


#### 终端下使用代理

- Linux, mac 代理配置

```
export http_proxy=http://username:password@site:port/
export https_proxy=http://username:password@site:port/
export HTTPS_PROXY=http://username:password@site:port/
```

可以将上面配置设置保存到终端配置文件(例如 ~/.bash_profile)里

- 关于 NPM 工具代理配置

不配置代理的话 NPM 很难愉快的使用

```
$ nam config set proxy http://server:port
$ nam config set https-proxy http://server:port
```

server:port 可以在你选择的代理服务商后台中心找到
