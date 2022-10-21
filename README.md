# 概述

这是一本 Xiaomi Redmi Note 8 Pro(begonia) 的刷机手册
本手册暂时不会提供英文版

[这是仓库链接](https://github.com/naranyinyun/RN8P-GUIDE)，如果你觉得不错，就给个star吧


> 编纂/构建 [纳兰音韵](https://nalanyinyun.ml)
> 
> 本手册由docsify强力驱动
> 
> 本项目由Cloudflare Pages托管
> 
> 本项目由Cloudflare提供加速和保护

!> 无论您是否按照本手册提供的方法刷入，设备产生的任何问题均与我们无关

?> 部分链接我会放在友情链接部分中，请善用**侧边栏**

!> <font color="Red">不要接受任何人的收费服务(最基础的)，切莫助长歪风邪气</font>

!> 你现在看到的绿色和红色信息框分别代表提示和警告,极具风险的警告我们会使用红色,<font color="Red">就像这样</font>

?> 需要验证码吗? RN8P-Docsify

我很喜欢一句话
> Troubleshooting any problem without the error log is like driving with your eyes closed.
>
> 在没有错误日志的情况下排查问题等同于闭眼开车

喜欢音乐吗?  
<meting-js
	server="netease"
	type="song"
	id="1809713119">
</meting-js>

# Recovery

## 通过ADB刷入第三方Recovery

首先，在您的电脑上配置好Adb环境，如果您不知道如何配置，可以参考[这篇文章](https://blog.nalanyinyun.ml/p/adb-flash/)

将手机重启至Fastboot模式并连接电脑

在您的终端中输入

```
adb flash recovery [filename/path]
adb reboot recovery
```

这样您的手机就会重启至Recovery了

!> 您的手机已经刷入了第三方Recovery，在不关闭avb的情况下无法启动

!> 一般情况下，MIUI会覆盖第三方Recovery，您可能需要刷入Magisk，签名Boot或使用Recovery自带的防覆盖功能

## 使用其他方法刷入第三方Recovery

您可以使用其他工具刷入Recovery，比如搞机助手，秋之盒，这些软件都提供简明易懂的GUI，我们不再介绍

?> 您可能需要从[憨憨初音酱](https://wxdowmloads.cn/)的下载站获取一些资源

# Magisk

## 通过第三方Recovery刷入

从GitHub[获取Magisk](https://github.com/topjohnwu/Magisk)并将其重命名为Install.zip(大小写不敏感)

重启设备至Recovery并使用MTP将install.zip传入手机

在Twrp(为例)中选择刷入，选择Install.zip刷入并滑动刷入

?> 如果需要卸载，将其重命名为UnInstall.zip刷入

!> Magisk自动关闭AVB，但我不确定每个版本都自动关闭，所以请您在刷入旧版时观察输出日志判断

## 通过Fastboot刷入修补的Boot

提取boot(您可以使用任何方式提取，比如线刷/卡刷包，终端提取)

打开Magisk Manager，选择安装，选择“选择并修补一个文件”，选择你的boot并等待修补完成

?> 修补后的boot和原boot在同一个目录

重启至Fastboot并刷入boot

?> 可以通过搞机助手等工具刷入，或者使用adb刷入，教程在配置adb环境那里的链接

!> 我并没有试过使用这种方式刷入Magisk，所以请您在无法启动设备时自行**关闭AVB**

!> <font color="Red">不要刷入其他人提供的boot,您无法确定它是否适用于您的设备</font>

## MIUI特色

MIUI的开发版可以获取root权限，您可以授予搞机助手root权限并使用转换功能刷入Magisk

!> Android11可能需要格式化data后才能正确关闭AVB，如果您无法启动设备，请自行关闭AVB

# 类原生和第三方ROM

## 基于Android11(MIUI12.5)的动态分区 非CFW ROM

!> 警告 本节所指的"动态分区"并不是Google指定出厂Android10及以上设备搭载的动态分区

?> 方法来自[憨憨初音酱](http://www.coolapk.com/u/3430069)，本章节只是稍作修改(大多是排版上的)

先决条件：

- 已解锁的设备
- 设备运行的是基于Android11的MIUI12.5(稳定/开发/国际版均可)
- 可以正常使用的电脑

步骤：

1. 下载并刷入动态分区专用的Recovery
2. 重启至Recovery并使用MTP将ROM传输至设备
3. 点击安装，选择ROM并滑动确认刷入
4. 点击清除，双清并格式化data

可选的额外步骤：

- 刷入Magisk
- 刷入GAPPS

?> 您可能需要跳过Google验证，在第三方Recovery终端内输入

```
dd if=/dev/zero of=/dev/block/by-name/frp
```

?> 您可以在刷入后直接刷入其他的**动态分区**ROM，只需格式化data和双清

?> Android12L下Recovery不解密，自备闪存卡或OTG

!> 如果您需要切换到其他非动态分区ROM，请线刷/卡刷回MIUI再刷入

## 基于Android11(MIUI12.5)的非动态分区 非CFW ROM

!> 本章节的方法我并没有尝试过，请您仔细甄别本章节的内容，如果你愿意帮助我们完善手册，可以到本项目的GitHub仓库编辑README.md，我们会在手册底部致谢部分填写您的名字

先决条件：

- 已解锁的设备
- 设备运行的是基于Android11的MIUI12.5(稳定/开发/国际版均可)
- 可以正常使用的电脑

步骤:

1. 刷入Android12的专用Recovery
2. 重启至Recovery并使用MTP传输ROM至设备
3. 选择ROM并滑动确认刷入
4. 双清并格式化data

关于其他的步骤，可以参考上一小节的方法，我有点懒得写了，~~李姐万岁~~

### 关于Android T(13)的☆特殊说明☆ 

目前的Android T ROM均基于MIUI12.5 Android R

这是刷入方法
1. 刷入[twrp](https://drive.google.com/file/d/1i491MVtCRM1lKFrJKLR7gr4uba67lIHk/view?usp=sharing) v3.6.2_12-4
2. 刷入ROM，双清，格式化data并重启

!> <font color="red">目前Android T的ROM均为静态构建，您必须卡刷/线刷回MIUI才能继续</font>

!> 目前**所有**Android T ROM都存在解码器问题，表现为硬解视频时卡顿，花屏，绿屏，别慌，您的设备没有出现问题

?> 目前没有第三方启动器适配Android T

?> 因为底层机制变更，大多数破解版软件无法使用

!> 在一些ROM上，刷入magisk重启后管理器会不识别，请您卸载后刷入magisk24.3

?> 在刷入任何模块前，请检查模块对Android版本的支持范围


# 后记

## 内容

不要着急，我们会逐步完善此手册的内容，如果您愿意帮助我们，可以到本项目的GitHub仓库编辑README.md
这是我们的仓库[地址](https://github.com/naranyinyun/RN8P-GUIDE)

?> 在提交PR时，请您允许所有者编辑，我们需要保持本手册的语言风格以及语法规范

## 讨论(~~社区~~)

我们在承载本项目的GitHub仓库开启了Discussions功能  
如果你有任何疑问或建议，可以直接发布Issue或Discussions  

## 链接

憨憨初音酱的[下载站](https://wxdowmloads.cn/)  
纳兰音韵的[博客](https://blog.nalanyinyun.ml)

## 致谢

### 内容贡献者

> 暂无

### 尾记

群星璀璨

--------

Powered By Docsify

Copyright 2022 Nalanyinyun/Wilderness. All Rights Reserved

本网站包含的内容使用[CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh)共享
