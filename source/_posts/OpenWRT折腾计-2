---
title: OpenWRT折腾记 - 2
date: 2021-03-24 12:56:47  
tags:  
- OpenWRT  
- Play
- Linux
- Synology
- NAS
- UPS
- NUT
categories:  
- Play  
- Router
  
---

前面帮那个哥们装完星际宝盒的OpenWRT之后，~~发现空载时的核心温度为80℃以上，于是我也想装一个体验一下~~，看到他的界面比Padavan好看，而且还支持KMS服务器什么的插件，然后我也给我的新三（NewWiFi D2）装了一个。
<!--more--> 
  
# 前言  

首先说明，我会尽量使用图形化界面来进行配置，因为命令配置通常是无记录且不可逆的。  

# 刷机
  
刷机就不说了，[恩山论坛](https://right.com.cn)上一大把自编译固件，但是我用的是官方固件，因为装各种包的玄学问题会尽量少（折腾那个哥们的OpenWRT已经充分让我感受到了什么叫玄学），在[这里](https://downloads.openwrt.org/releases/19.07.7/targets/ramips/mt7621/)找到`d-team_newifi-d2-squashfs-sysupgrade.bin`，注意一定要是`squashfs-sysupgrade`的，另一个真的是纯净版系统，啥都没有，连WiFi驱动都得自己装的那种，很不推荐。这个有一些基本的功能，算是一般定义的纯净了。  
  

# 换源  

装好之后，就可以换软件源了，参考[清华源使用帮助](https://mirror.tuna.tsinghua.edu.cn/help/openwrt/)更换源，由于我校校园网使用DrCOM进行认证，所以现在还没有网络，需要先手动安装`dogcom`和`luci-app-dogcom`，`dogcom`的手动编译我上篇博客已经说得很明白了，不再赘述；况且`dogcom`作者[mchome](https://github.com/mchome)Release了一个`misp_24kc`的版本出来，适用于新三、小米AC2100等。我是这样安装的，首先在电脑上下载插件，进入到插件目录，`Shift+右键`呼出菜单，然后再点击`在此处启动PowerShell`，输入`python -m http.server`，这要求您的电脑有Python环境。然后在路由器中看自己的IP或者使用主机名，我这里使用主机名，命令如下： 
  
```bash
opkg install http://EvydePC:8000/dogcom.ipk
opkg install http://EvydePC:8000/luci-app-dogcom.ipk
```
  
或者您也可以在LUCI界面的`系统->软件包`处上传软件包并安装。 
配置好Dogcom之后，就能上网了。首先打开，点击`更新列表...`来更新软件源，当然您也可以使用`opkg update`来更新。  
# 扩容  

我觉得新三的闪存不太够，于是插了一个U盘（也为后来部署NUT工具留下了伏笔），下面就是把软件包安装目录挂载到U盘了，参考[这篇文章](http://www.likecs.com/default/index/show?id=114959)即可，但是原文有些命令格式不太对，我这里重新引用一下命令（这些软件包也可以在图形化界面里安装，但是因为图形化界面和这个同步，所以这样安装也可以）：
  
```bash
# 安装插件
opkg install fdisk swap-utils kmod-usb-storage kmod-fs-ext4 e2fsprogs kmod-usb-ohci kmod-usb-uhci  block-mount

# 使用fdisk对U盘进行分区，/dev/sda是U盘
fdisk /dev/sda
# 依次输入以下字符
p
d # 删除U盘分区
n
p
1 # 分区数量
<回车> # 默认分区起点
<回车> # 默认分区尾部
w # 保存配置
# 格式化
mkfs.ext4 /dev/新建分区的名字  # 一般sda

# 挂载
mount /dev/sda /mnt/sda
# 如果提示没有找到文件夹，可以先使用mkdir /mnt/sda建立文件夹
cd /mnt/sda
ls
# 显示结果lost+found即为成功
# 迁移/overlay数据
cp -r /overlay/* /mnt/sda  # sda是新建分区的名字
# 最后查看/mnt/sda目录下是否有了/overlay目录的数据,有则成功
```
  
建议重启路由器，再在图形化界面里进行挂载，具体在`系统->挂载点`，然后点击添加，选择U盘设备（通过大小可以判断），此时应该会只有一个选项就是`挂载点`，选择`作为外部 overlay 使用（/overlay）`，顺便把启用的勾打上，保存并应用，最后建议重启一下。 

# 换主题  

这里推荐[Argon](https://github.com/jerrykuku/luci-theme-argon)，博主列出了详细的安装方法，这里不再赘述，就是一定要注意一下`LEDE`系统和`OpenWRT`系统的插件不一样。装完之后记得装配套的配置插件。换完之后可能报错，装一下`luci-compat`就好了。

# 汉化  

首先，在`系统->语言和界面`里面选择对应的主题和语言，然后，安装能安装的所有软件包的对应汉化包，比如系统自带软件`firewall`，在软件包搜索的时候发现其有一个`luci-i18n-firewall-zh-cn`的汉化包，安装所有能安装的以`luci-i18n`开头`-zh-cn`结尾的汉化包。

# 插件  

## 官方插件  

我这里列出的，都是软件源里有的插件。我直接先列出命令：

```bash
opkg install miniupnpd nlbwmon nut nut-common nut-upslog nut-upsmon nut-upssched luci-app-autoreboot luci-app-nut luci-app-nlbwmon luci-app-upnp
```

|插件名称|作用|
|:--:|:--:|
|luci-app-autoreboot|设置定时重启|
|luci-app-nut, nut, nut-common, nut-upslog, nut-upsmon, nut-upssched|Network UPS Tools(NUT)管理NUT工具|
|luci-app-nlbwmon, nlbwmon|流量统计|
|luci-app-upnp, miniupnpd|UPnP管理|

官方的就这些，记得装汉化包。  

## 第三方插件  

这里列出的，都是网上找的插件，很不稳定，甚至有的插件作者已经不再更新，但是有另外的开发者fork到他那里更新，比如`vlmcsd`。  
还是先上命令：
  
```bash
opkg install vlmcsd frpc luci-app-vlmcsd luci-app-frpc
```

|插件名称|作用|
|:--:|:--:|
|luci-app-frpc,frpc|Frpc内网穿透，作者唯一且仍在更新|
|luci-app-vlmcsd, vlmcsd|KMS服务器，用于自动激活内网MicroSoft产品，作者已停止更新，第三方开发者仍在更新|

好像我听说还有一个JetBrains全家桶激活的，不过我没有相关需求就没装。 以及老生常谈Clash，我只能说OpenWRT上的OpenClash非常阴间，完美诠释了`Open`这个词，这个OpenClash甚至不如老毛子固件的好用。如果非要用，建议用ShellClash，或者和我一样在另一个设备上装ShellClash，按需手动切换，具体还是见我之后的博客。  

## 配置  

这些插件都需要配置，大多数按默认配配置可以很好地工作，这里主要说一下NUT的配置，尤其是和群晖搭配使用，这个我打算单开一篇博客说，顺便说一下群晖的配置。

# IPv6配置  

教育网IPv6一直是个老大难问题，我一直在找一个较为完美的解决办法，网上一共有三种办法，第一是NAT转发，但是我觉得这样相当不妥，违背了IPv6的初衷；第二种是路由器桥接，就是把所有IPv6包直接交给上游处理，这样虽然比较稳定，但是有两个问题：日志里会产生一大堆错误、路由器本身没有IPv6地址。第三种就是利用自带的DHCPv6客户端进行管理了，这里介绍的也是这种办法。  
我之前看教程，一直不


# 杂项配置  

## NTP  
~~NTR~~ NTP服务器

## 管理权限  


## 防火墙  


## 端口转发/UPnP  


## 密码  


## 静态DHCP地址  


## 
