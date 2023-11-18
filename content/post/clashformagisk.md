---
title: 'ClashForMagisk安装及避坑'
date: 2023-07-30T10:27:37+08:00
description: ClashForMagisk是一款基于magisk的clash网络调试工具，相较于ClashForAndroid占用及功耗更低。如果你连magisk和root都没有听说过的话，我还是建议您使用ClashForAndroid。
tags:
    - 网络通讯
    - Magisk
---
# 宇宙安全声明
本教程内所有内容禁止用于任何对国家不利的事情总，ClashForMagisk只是个网络调试工具，请不要用于非法事业，本人概不负责。  
龙的传人需自律，坚决维护国家和平统一，坚持党的伟大领导。


# 准备
ClashForMagisk repo: https://github.com/taamarin/ClashforMagisk  
下载直达: https://github.com/taamarin/ClashforMagisk/releases/latest  
Dashboard: https://t.me/MagiskChangeKing/159

请确保你已经刷入magisk！


# 教程开始
## 刷入ClashForMagisk
点击模块 - 然后和其他模块一样刷入

## 安装Dashboard
不建议使用在releases里那个ClashForMagiskManager，因为会不停地跳获取root权限，很烦。

## 重启


# 配置环节
我们来看看官方README怎么说（无关紧要的内容我直接删除了）


## subscription
you can use SubScription

open /data/clash/clash.config line 29-34  
`update_interval="interval contab"`  
`Subcript_url="your_link"`  
`auto_updateSubcript="true"`

这些是一些配置项 第一个为更新时间 第二个为订阅链接 第三个为是否自动更新

Running manual command
```
${MODDIR}/scripts/clash.tool -s
```

Config Online  
clash.config line 36-37, If true, use it to download the subscription configuration, when starting Clash , So no need to type `${MODDIR}/scripts/clash.tool -s` anymore  
打开之后每次开启clash会自动更新订阅

## Change Clash kernel
You can use Clash.Premium and Clash.Meta  
这里是教你怎么切换内核的，我推荐使用Clash.Meta，开源且功能强大

Clash Meta  
`/data/clash/kernel/lib/Clash.Meta`  
Clash Premium  
`/data/clash/kernel/lib/Clash.Premium`  
you can download the Kernel automatically, for the settings in the clash.config line 79-103

```${MODDIR}/scripts/clash.tool -k```

## GeoSite, GeoIP, and Mmdb
settings are in clash.config line 105-116  
if true, will be updated every day at 00.00  
you can change the URL  
自动更新GeoIP信息


# 避坑环节
注：以下功能在ClashForMagisk的PreRealse版本似乎已经实现了，仅对3.0及以下版本有参考意义。  
由于没有正确配置UA（及UserAgent），导致使用下载订阅功能下载二代机场订阅时下载下来的是经过base64加密的v2ray订阅，ClashForMagisk无法直接识别。  
因此，我们需要为`clash.tool`文件中的wget指令添加一个UA。

找到`/data/clash/scripts/clash.tool`，通过搜索找到`update_file()`这一功能在下面两句wget指令后添加
```
-header="User-Agent: ClashForAndroid/<2.8.7>"
```
其中`2.8.7`可以替换为任意ClashForAndroid版本号。  
然后使用
```
/data/clash/scripts/clash.tool -s {你的订阅链接}
```
进行手动更新订阅（如果你将你的订阅链接放在`/data/clash/clash.config`里就不用再输入了）
