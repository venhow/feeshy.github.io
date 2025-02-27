---
layout: post
title: 折腾记录：用iOS快捷指令复刻Pushbullet
date: 2020-08-26
last_modified_at: 2023-08-03
tags:
  - 快捷指令
  - shortcuts
  - pushbullet
  - 折腾记录
redirect_from:
  - https://meta.appinn.net/t/topic/18629
toc: true
---

Pushbullet曾经是一个全平台的跨设备消息推送服务。开发者由于不满iOS的封闭性而长期停更，最终借着苹果强推Apple ID登录的契机彻底下架了iOS客户端。

这次尝试用[Pushbullet官方API](https://docs.pushbullet.com/) 和[快捷指令](https://support.apple.com/zh-cn/guide/shortcuts/apd58d46713f/ios)复刻一个低配版的Pushbullet

- 功能
	- 从iOS推送文本或链接到其他设备
	- 一键获取其他设备发给iOS的最新一条推送
- 优势
	- 不存在下架问题
- 缺陷
	- 不能以“真正的”推送通知形式接收推送，而是要主动执行快捷指令
	- 由于快捷指令没有提供适合展示历史记录的界面，暂未加入查看推送历史的功能

## 依赖的工具

- iOS：[快捷指令](https://apps.apple.com/cn/app/id915249334)
- 其他平台：官方客户端——[Chrome](https://chrome.google.com/webstore/detail/chlffgpmiacpedhhbkiomidkjlcfhogd) | [Firefox](https://addons.mozilla.org/en-US/firefox/addon/pushbullet/versions/) | [Android](https://play.google.com/store/apps/details?id=com.pushbullet.android) | [Windows](https://update.pushbullet.com/pushbullet_installer.exe)
- 科学上网工具：`pushbullet.com`加入代理规则

---
## 配置

### 1. 获取Access Token

登录账号后访问 [https://www.pushbullet.com/account](https://www.pushbullet.com/account) 生成API令牌

![screenshot](/assets/img/push_gen_token.png)

### 2. 获取设备ID

> 如果你并不想对各台设备进行区分，则无需获取设备ID便可直接进入第3步。

如果想要精准地推送或接收某台设备的消息，我们需要先知道它的`device_iden`。

访问Pushbullet API可以获取所有曾经登录过Pushbullet官方客户端的设备的ID。如果你已经错过了Pushbullet官方iOS App的上架时间，在获取到的列表中自然就找不到你的iOS设备，这种情况也可以向API请求生成新的设备ID。

#### 省事方式

推荐使用这个[一次性快捷指令](https://www.icloud.com/shortcuts/b763a6cc3b834caeabeb2cf0b9e7a1c8)完成这两个过程，用完即删。

#### 其他方式

你也可以使用任意其他的HTTP调试工具，例如Pushbullet API 官方文档示例的_curl_

##### 获取已有iden

```
curl --header 'Access-Token: <your_access_token_here>' \
     https://api.pushbullet.com/v2/devices
```

甚至可以直接用浏览器访问 [`https://api.pushbullet.com/v2/devices`](https://api.pushbullet.com/v2/devices) ，用户名填第一步获取的Access Token，密码留空，服务器会返回一段**没分行**的纯文本。

用你的火眼金睛在其中找到你的iOS、Android、Chrome等等设备的iden并记录。你可以用[JSON Beautify工具](https://codebeautify.org/jsonviewer) 将JSON自动分行，提高搜寻的效率

##### 生成新的iden

```
curl --header 'Access-Token: <your_access_token_here>' \
     --header 'Content-Type: application/json' \
     --data-binary '{"app_version":8623,"manufacturer":"Apple","model":"iPhone 5s (GSM)","nickname":"Elon Musk's iPhone","push_token":"production:f73be0ee7877c8c7fa69b1468cde764f"}' \
     --request POST \
     https://api.pushbullet.com/v2/devices
```

### 3. 配置快捷指令

成品有两个版本：

- 推送接收二合一版
    -  [推送&接收Shortcut](https://www.icloud.com/shortcuts/0dfcecfcbca046a98980ef826d4825e9)：推送共享表单，或提取收到的内容，**无推送剪贴板功能**
- 独立版
    -  [推送Shortcut](https://www.icloud.com/shortcuts/a44bcaf20bc74139ade91abde00ebaa9)：推送共享表单或**剪贴板**中的内容
    - [接收Shortcut](https://www.icloud.com/shortcuts/921b57d61ed34955a87c1bb30261fa99)：提取收到的内容

<details><summary>更新日志</summary>
- 2020/8/26: 初始发布
- 2020/9/30: 现在可以获取其他设备发送给iOS的推送，可使用独立的接收Shortcut或者二合一的Shortcut
- 2020/11/2: 修复了无法正确判断url的问题
</details>

首次运行快捷指令前需要填入三个字段

- `access_token`: 第一步获取的令牌
- `this_device_iden`: 第二步获取或生成的iOS设备本机的`device_iden`
- `remote_device_iden`: 第二步获取的其他设备的`device_iden`（例如Chrome、Android）

> 如果你跳过了第二步，那么请把所有“获取URL内容”步骤中的 `device_iden` 和 `source_device_iden` 字段删除，自行添加 `email: 你的账号`字段

![screenshot](/assets/img/push_api_access.jpeg)

---

## 使用

快捷指令提供三种入口：小部件、主屏幕图标、共享表单

| |共享表单|小部件和图标|
|---|---|---|
|二合一版|推送传入的链接或文本|一键提取发送给本机的最新一条推送|
|独立版|推送传入的链接或文本|推送剪贴板中的链接或文本  <br>一键提取发送给本机的最新一条推送|

你甚至可以自定义图标制作一个以假乱真的“[自定义图标](https://lh3.googleusercontent.com/I1rEarjkcHM2Yq13tYxJtg8idaYLK6kGXI0AMSm5VLMl5_nPwVuR4UFhAOSZo83CBe8)Pushbullet客户端”

![screenshot](/assets/img/push_shortcuts.jpeg)  

---

## 延伸：一键转发验证码的实现思路

iOS14更新中，快捷指令的**伪**自动化新增了“收到短信”的触发条件

我们可以以此建立一个**伪**自动化。当收到包含验证码的短信时，提取出验证码，调用上面的指令推送到Chrome、Android等其他设备

![screenshot](/assets/img/push_sms.jpeg)

不过在实际收到短信时，快捷指令只是弹出一条通知，要我们拿起手机点击通知才能执行

因此这只能算是分享一个思路，由于快捷指令自身能力的限制，并没有实用的价值。一旦iOS15、iOS16引入了**真**自动化，这个思路就可以实际应用了