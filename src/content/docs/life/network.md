---
title: 校园网络
---

## 校园网

### 开发区校区校园网

[开发区校区上网登录过程指引说明](https://eda.dlut.edu.cn/info/1592/43102.htm)

关于校园网：宿舍每个人有一个有线网口，校内各楼宇也有几乎全覆盖的 WiFi。价格方面，每月 20 元 150GB 流量，通过大工学生系统 SSO 登陆使用。网速方面，IPv4 限速 100 兆，IPv6 有线连接下理论速度最高为千兆，实际上由于信号衰减等最高大概在三百~六百兆左右） 。另外实验室、创中的 WiFi 不限量。或者去机房也能蹭免费网络。

PS：在每年的大型考试期间（比如高考中考），由于校区北邻职业中专南邻开发区一中，信号屏蔽会非常到位，严重影响移动数据等网络连接，校园网基本不受影响。

### 主校区校园网

[学生上网服务使用方法](https://its.dlut.edu.cn/index/jsfw/fwzn/xywf/xsswfw.htm)

### 校园网自助报障

由于各校区的校园网服务不互通，如果在使用中遇到了网络连接、设备故障等问题，请咨询当前所在校区的网信中心工作人员。

开发区校区的同学可以通过校园网自助服务系统中的“自助报障”功能进行反馈，或发送邮件至 kfqit@dlut.edu.cn 或拨打电话 0411-62274385 进行反馈。

### WebVPN


[校园网VPN服务使用说明](https://its.dlut.edu.cn/index/jsfw/fwzn/VPN/vpn.htm)

### 校园网免流







[校园网ipv6免流](https://bing.com/search?q=%E6%A0%A1%E5%9B%AD%E7%BD%91ipv6%E5%85%8D%E6%B5%81)

## 校园卡

校园卡是各大运营商提供的一种带学生优惠套餐的 SIM 卡，和大连理工大学**没有任何关系**，无法直接使用大连理工大学校内网络资源且不受校园网管控。说白了就是流量卡（甚至还不如流量卡，因为有校园基站的限制）。

## DNS

## NTP（授时服务器）

出于不明原因，大连理工大学校园网阻断了来自外部的 IPv4 NTP 流量，而大工自己的 NTP 服务器（time.dlut.edu.cn，IP 地址为 202.118.66.180）无论是 IPv4 还是 IPv6 连接下同步时间都是正常的。如要使用外部 NTP 服务器，需要有 IPv6 网络连接，或不使用大连理工大学校园网。

### Windows 客户端配置

#### Windows XP 及以下版本的授时服务器配置

在“运行”中输入 `net time /setsntp:time.dlut.edu.cn`。

#### Windows Vista 及以上版本的授时服务器配置

在“控制面板 > 时钟、语言和区域 > 日期和时间 > Internet时间 > 更改设置”中勾选“与 Internet 时间服务器同步”，在“服务器”一栏填入 `time.dlut.edu.cn`。

也可通过在命令提示符中使用 `w32tm /config /manualpeerlist:"time.dlut.edu.cn" /syncfromflags:manual /reliable:yes /update` 来将此服务器设置为当前电脑的授时服务器。

### Linux 客户端配置

使用 systemd-timesyncd 的用户需修改 `/etc/systemd/timesyncd.conf`，将其中 `NTP=` 一行取消注释，修改为 `NTP=time.dlut.edu.cn` 。

使用 ntpd 的用户需要在 `/etc/ntp.conf` 中添加一行 `server time.dlut.edu.cn` 。（若你的发行版使用 Chrony，请修改对应的配置文件 `/etc/chrony.conf`。）

为了确保 ntpd 服务正常运行，使用你当前发行版的 initscripts 脚本或 `systemctl`（若有）进行检查和修正。

如果你的机器的时钟发生跳变不会导致严重后果，你可以使用 `sudo sntp time.dlut.edu.cn` 进行一次性的同步。

### Mac 客户端配置

在“系统配置 > 日期与时间 > 自动设置日期与时间”一栏，填入 `time.dlut.edu.cn`。

在 macOS Mojave 及更新的系统，你可以使用 `sudo sntp -sS time.dlut.edu.cn` 来进行一次性的同步，否则，使用 `sudo ntpdate time.dlut.edu.cn` 进行同步。

