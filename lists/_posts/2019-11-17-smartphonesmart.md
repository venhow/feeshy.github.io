---
layout: post
title: feeshy的自动化配置
date: 2019-11-17
last_modified_at: 2024-3-12
tags:
  - tasker
  - 快捷指令
  - autohotkey
  - 折腾记录
redirect_from:
  - /tech/smartphonesmart.html
---

## <img src="https://tasker.joaoapps.com/icon_tasker.png" style="display:inline;height:1em;vertical-align:middle;"> Tasker

### [微信的高级响铃控制](https://github.com/feeshy/tasker_profiles_share/blob/master/Wechat_Alerts/readme.md)

尝试修复微信Android版在勿扰模式下仍然能响铃的bug，并赋予其更高级的响铃控制。

### [抖音快手音量标准化](https://github.com/feeshy/tasker_profiles_share/blob/master/TikTok_Normalizer/readme.md)

刷抖音、快手时自动将媒体音量降低30%，退出时恢复原来的音量

### [定时切换日/夜模式](https://github.com/feeshy/tasker_profiles_share/blob/master/Night_Mode/readme.md)

定时切换夜间模式、免打扰、系统音量、同步、飞行模式（其中飞行模式切换需要root权限）

### [日租卡自动关数据](https://taskernet.com/shares/?user=AS35m8kd%2B%2B8TCtuKD5vi%2BgxDuL5p9VAa8vrSP6viIGO6nBMQGv6ntB%2BfsCHAjiN7MZx1YA%3D%3D&id=Profile%3A%E8%87%AA%E5%8A%A8%E5%85%B3%E6%95%B0%E6%8D%AE)

在每月21日~月底的午夜自动关闭移动数据开关，防止不知不觉中开启下一天计费。可根据实际情况自行调整生效日期的范围

### [未接来电转发](https://github.com/feeshy/tasker_profiles_share/blob/master/Pushbullet_Intergrated/readme.md#%E6%9C%AA%E6%8E%A5%E6%9D%A5%E7%94%B5%E8%BD%AC%E5%8F%91)

使用Pushbullet或短信将Android手机的未接来电发送至另一台手机。

### 短信转发

将一台Android手机所接收的短信转发至另一台手机：  
[用Bark或短信转发验证码](https://github.com/feeshy/tasker_profiles_share/blob/master/Bark/readme.md#%e8%bd%ac%e5%8f%91%e9%aa%8c%e8%af%81%e7%a0%81) | [用Pushbullet或短信转发](https://github.com/feeshy/tasker_profiles_share/blob/master/Pushbullet_Intergrated/readme.md#%E7%9F%AD%E4%BF%A1%E8%BD%AC%E5%8F%91) | [仅用短信转发](https://github.com/feeshy/tasker_profiles_share/blob/master/Offline_SMS_Forward/readme.md#%E9%80%82%E5%90%88%E5%8F%8C%E5%8F%B7%E5%8F%8C%E6%9C%BA%E7%9A%84%E7%A6%BB%E7%BA%BF%E7%9F%AD%E4%BF%A1%E8%BD%AC%E5%8F%91)

### [Pushbullet远程短信](https://github.com/feeshy/tasker_profiles_share/blob/master/Pushbullet_Intergrated/readme.md#%E8%BF%9C%E7%A8%8B%E7%9F%AD%E4%BF%A1)

Pushbullet提供用PC或者平板遥控安卓手机发短信的功能，但你无法用一台手机遥控另一台手机发短信。本profile尝试补齐此需求。

### [Push to Bark](https://github.com/feeshy/tasker_profiles_share/blob/master/Bark/readme.md#%E6%8E%A8%E9%80%81%E9%93%BE%E6%8E%A5%E6%88%96%E6%96%87%E6%9C%AC)

从通知栏磁贴、文本选择菜单、分享菜单等入口运行，把传入的或者是剪贴板中的链接、文本推送到[Bark App](https://apps.apple.com/cn/app/id1403753865)。

### [Aria2 离线下载](/tech/aria2)

将Android上的链接发送到VPS、NAS等远程设备上的Aria2进行离线下载

## <img src="https://help.apple.com/assets/5D38A6ED0946225A2D640948/5D38A6F70946225A2D640958/zh_CN/18c714c61bfdebca44fe6989f0a2511d.png" style="display:inline;height:1em;vertical-align:middle;"> iOS快捷指令

集中下载：[240329](https://www.icloud.com/shortcuts/005d95cd4acd42f2a44742036d30407b)

### [Pushbullet for iOS](/tech/pushbullet)

在iOS与其他平台的Pushbullet官方客户端之间推送链接和文本

### Push to Bark

Bark是一个简单好用的推送接收App。这个指令使你可以用iOS设备向Bark发送链接或文本，虽然我也不知道这到底有什么用

### Aria2远程下载

将iOS上的链接发送到VPS、NAS等远程设备上的Aria2进行离线下载

### 网易云下载

通过共享表单或者粘贴分享链接的方式下载网易云音乐中的歌曲到本地，并进行重命名。也可以配合上面的Aria2远程下载进一步

### 在浏览器打开或搜索

三合一的浏览器增强工具。共享图片URL以图搜图，共享其他URL转到URL，共享文本划词搜素。从小部件打开则搜索输入的内容

### 1688找货

二合一的浏览器增强工具。共享图片URL以图搜图，共享文本划词搜素。从小部件打开则搜索输入的内容

### WolframAlpha

WorlframAlpha是一个直接返回结果的知识搜索引擎。从小部件访问时本快捷指令作为一个书签打开WolframAlpha首页，从共享表单访问则直接搜索传入的文本

### 小本本

聚合剪贴板，将共享表单或者剪贴板的内容记到小本本上，每次记一行，记完统一提取

### 音视频转码

多合一媒体转码工具，目标格式包括AAC/HEVC/H.264/GIF

## <img src="https://www.autohotkey.com/static/ahk_logo_no_text.svg" style="display:inline;height:1em;vertical-align:middle;"> AutoHotkey

通俗易懂的AutoHotkey脚本使用方法

0.  安装[AutoHotkey](https://autohotkey.com/)
1.  新建一个`.ahk`后缀的文件
2.  用记事本打开这个`.ahk`文件
3.  粘贴脚本
4.  保存，然后把`.ahk`文件复制到  
    `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`

### [鼠标侧键增强脚本](https://meta.appinn.net/t/topic/17914)

这个脚本适合五键以上的鼠标。这种鼠标侧面的前进、后退键的使用频率要比常用的左、右、中键低不少。这个脚本将为这两个按键重新分配功能

### [还我Home/End/PgUp/PgDn](https://meta.appinn.net/t/home-end-pgup-pgdn/17801)

联想、华为、小米等品牌笔记本的键盘布局Home End键位设定过于反人类。这个脚本旨在缓解左手按Fn、右手按方向键的手忙脚乱

### [Bark.ahk](https://meta.appinn.net/t/autohotkey-bark/18677)

用一个快捷键选中的链接或文字推送到Bark App。可与前面的Pushbullet快捷指令搭配互补使用，实现双向推送

### [Calendar Wallpaper](https://meta.appinn.net/t/google-calendar/18376)

定期将日历截图并设置为壁纸。笨方法，依赖以下工具：UWP日历、AutoHotkey、ImageMagick、任务计划

## JavaScript

### [PPI计算器](/ppi-calc)

计算PPI，读取CSS分辨率，并对高DPI设备给出缩放建议。可能不定期更新加入新的功能

### [Ingress Link Distance计算器](/portal-calc)

根据给定条件计算可在[Ingress](https://ingress.com/)中建立的Link的最大连接距离，提供多种快捷输入预设。项目已开源，[fork it on github](https://github.com/feeshy/portal_calc_html)
