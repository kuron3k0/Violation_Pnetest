# 渗透红线Checklist

**很尬的事，手速过快把Pentest打成Pnetest，不过没什么影响，重点是内容的真实性、可用性。**
<br>
多人协作的渗透项目中，往往每个人擅长点和经验都不同，那么团队有一个人误操作很有可能会带来很严重的后果，导致入口打点被发现，或者内网渗透被监测到。<br>
这份Checklist需要遇到实战足够的坑才能形成这份文档，所以发起邀请**渗透师同共完成** "渗透操作红线列表"。<br>
在**Issues**提交，经过审核有价值的，才会添加进来。<br>

## 工具篇

* WebShell不能使用普通一句话木马，连接端使用加密流量，不使用普通中国菜刀。
* 不使用默认冰蝎，已被安全厂商能够识别流量（使用默认，入口打点这么辛苦，连接一小时就被发现，并被清除封堵）
* 上传工具到服务器中，不能使用默认名称，例如，frp、nc、lcx等。
* 使用sqlmap要加--random-agent参数。
* nmap、zmap扫描要去除特征。
* 不要相信工具的判断，工具测试一遍，手工测试一遍。
* sqlmap注入频率问题，使用--delay、--safe-url、--safe-freq    | ID：SewellDinG提供
* Cobalt Strike的Beacon证书和特征，如果使用默认的将会被检测。
* Cobalt Strike使用域前置技术，伪装成白站域名，隐藏真实C2服务器IP；（默认启动的CS,基本被各厂商设备能识别到） | ID：SewellDinG提供
* 在进行有可能导致管理员察觉的敏感操作时（如登录远程桌面等），根据目标所在地区，选择对应IP登录。（有些会提示异地登录提醒） ｜ID: evilAdan0s 提供
* 时区选择非大陆，作业时间贴合时区   ID：hmoytx提供
* 使用自己塔建的DNSlog，目前网上dnslog站点已被监控，只要请求了域名就会被监测到。 ｜ID: mx7krshell
* 在内网渗透时，关掉BurpSuite被动扫描。否则自己无意识访问网站会发起Fastjson、Shiro探测导致被安全设备检测到。 ｜ID：mx7krshell
* burp挂代理时关掉`http://burp`页面（proxy->options）和`http://burpsuite`（从代理层设置），以及代理报错信息

![](./burpinfo.png)

* burp选择自定义的tls信息，防止ja3指纹识别

![](./burptls.png)

## 安全意识篇

* 渗透工作电脑浏览器不能保存任何个人信息，防止被抓取信息。
* 不随意修改管理员密码、后台密码。
* 大文件需要打包分割下载。
* 不使用国内VPS（阿里云、腾讯云）做CobaltStrike远控服务器。
* 渗透项目结束后，不要继续进行测试。
* 开发代码中不要留个人id，生成木马的时候不要在个人电脑生成，会带上电脑路径、电脑名称。
* **永远用虚拟机操作，不要用真实机操作**
* **虚拟机快照，不必装杀软，完成项目后恢复一次快照**
* 电脑语言，用日语，英语，繁体字，不要用中文（看项目需要，一般用不上。）
* 设置路由器只允许1723等其它VPN端口才能出网，一但VPN断开将自动断网，不然在扫描过程VPN断开会暴露真实IP地址（看项目需要，一般用不上。）
* 从目标拖回来的任何文件都不要在有网的机器打开，要在专用脱网机打开。
* 渗透物理机脱网（用于存储文件，信息等），网络流量从虚拟机搭建的网关走usb网卡+匿名线路（看项目需要，一般用不上。）
* 注册网站需要验证码，使用接码平台。
* **高管邮箱、运维人员邮箱，发现有VPN帐号或者重要系统登录地址，访问需谨慎，特别是登录需要下载控件，"安全登录控件.exe"等等**
* **Github收集目标信息时，需要特别关注项目更新时间节点，如果较为新的话，访问需谨，有可能是引诱攻击者进入沙箱。**

## 暂未分类

* 多养一些仿大厂的域名，平时指向谷歌或者8.8.8.8，用的时候解析到自己服务器，不用的时候立马修改。（如果临时去注册域名或者短期内想要使用域名，会浪费很多时间在这上面，甚至能被安全设备检测，这是常有的事情，需要平时多储备，提升域名的可信度。） ｜ID：protonarm-ossr
* 记住自己上传的木马，保留好地址，项目结束后一定要删除或者提交，避免项目结束忘记清除被防守方发现，这锅很难说得清的。
* 在授权项目中，使用爬虫的过程中会做一些误操作，导致对网站不可逆的影响（爬取链接时，特别是已登录的状态下，爬取到delete页面会导致数据被删除） | ID: cangqingzhe提供
* 清理日志时需要以文件覆盖的方式删除文件，防止数据恢复，或者仅删除指定ID的日志. | ID：zhuotougg
* 一个团队，一定要团结一心，相互包容，互相帮助学习和进步，不要勾心斗角。否则这团队个人再厉害也是一盘散沙。
* 所有浏览器升级到最新版本，禁止使用旧版谷歌浏览器 ｜ ID: _得闲饮茶_
* 有反蜜罐插件anti-honeypot，工具都是不可信的，防守方把靶标伪装成蜜罐 | ID：mx7krshell

