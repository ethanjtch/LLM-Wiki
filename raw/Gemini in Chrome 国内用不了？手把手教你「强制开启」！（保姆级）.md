---
title: Gemini in Chrome 国内用不了？手把手教你「强制开启」！（保姆级）
source: https://blog.csdn.net/weixin_40774379/article/details/157622775
author:
  - AI信息Gap
published: 2026-02-02
created: 2026-07-10
description: 文章浏览阅读8.3k次，点赞13次，收藏17次。Gemini in Chrome 国内用不了？手把手教你「强制开启」！（保姆级）_chrome gemeni 没有图标
tags:
  - clippings
---
话接上文。

前情提要看这里：反击 OpenAI ！谷歌史诗级更新：Gemini in Chrome 正式上线，免费用

`Gemini in Chrome` 正式发布了，但你打开 Chrome，右上角压根看不到那个 Gemini 图标？

![](https://i-blog.csdnimg.cn/img_convert/7e025560622cc9c53460fadc347f0888.png)

怎么才能用上？

今天从原理到方法，一文讲清楚。

---

### 01｜先看谷歌官方怎么说

根据谷歌官方的 FAQ 文档，使用 `Gemini in Chrome` 需要满足这些条件。

> - Be 18 or over and in the US.
> - Use a Chromebook Plus, Mac, or Windows computer.
> - Use the latest version of Chrome.
> - Sign in to Chrome.
> - Have Chrome's language set to English (United States).

![](https://i-blog.csdnimg.cn/img_convert/96336297c39a59fe1ed4f3b1d3c19ab3.png)

总结一下就是五点要求。

年满 18 岁且在美国。使用 Chromebook Plus、Mac 或 Windows 电脑。Chrome 更新到最新版本。登录 Chrome。语言设置为英语。

前四条好办。最后一条也好办，在设置里改就行。

真正的问题是第一条。

「在美国」这三个字，Chrome 是怎么判断的？

---

### 02｜先试最简单的方法

在折腾之前，先试一下 Chrome 自带的实验性功能开关。

在地址栏输入 `chrome://flags/` ，搜索 `glic` 。

你会看到好几个带 `Glic` 的选项，全部从 Default 改成 Enabled，然后点右下角重启 浏览器 。

![](https://i-blog.csdnimg.cn/img_convert/4c85af71c9aabd0f006bd1b6593dc61b.jpeg)

重启后看看右上角有没有 Gemini 图标。

有的话，恭喜你，成了！

没有的话，打开 Chrome 设置，找到 `AI innovations` -> `Gemini in Chrome` ，手动打开。

首次使用会弹出条款，同意就能用了。

![](https://i-blog.csdnimg.cn/img_convert/1c4375e3b5d8616df5ee78ada9a2ef28.jpeg)

都不行，继续往下看。

---

### 03｜为什么 flags 不一定管用

Chrome 判断用户地区用的是多重验证。

IP 只是其中一环，更关键的是浏览器本地存储的「地区标识」。

这些信息存在一个叫 `Local State` 的配置文件里。

Chrome 每次启动都会读取这个文件，决定给你推送哪些功能。

`Gemini in Chrome` 的内部代号就是 `glic` （所以上一步可能有用）。

Chrome 会检查一个叫 `is_glic_eligible` 的字段，如果是 `true` ，才会显示 Gemini 图标。

在非美国地区首次安装的 Chrome，这个字段要么不存在，要么是 `false` 。

地区标识也会被设成所在的地区。

所以即使你在 flags 里手动启用了 `glic` ，Chrome 依然有可能认为你「没资格」。

对应的解法就是手动修改这个配置文件。

---

### 04｜修改 Local State 文件

这个文件的位置因操作系统而异。

#### Mac 用户

```cobol
~/Library/Application Support/Google/Chrome/Local State
```

#### Windows 用户

```sql
%LOCALAPPDATA%\Google\Chrome\User Data\Local State
```

文件没有扩展名，内容是 JSON 格式。用 VS Code、记事本或任何文本编辑器都能打开。

改之前先把 Chrome 彻底关掉。

Mac 按 `Cmd+Q` ，Windows 右键退出。

打开 Local State 文件，搜索并修改这两个字段。

先是让 Chrome 认为你在美国。

```csharp
"variations_country": "us",

"variations_permanent_consistency_country": ["145.0.xxxx.xx", "us"]
```

第二个字段是个数组，第一项填你的 Chrome 版本号，第二项填 "us"。

![](https://i-blog.csdnimg.cn/img_convert/ccd13d294098eb6aee11b8c4183ef2ad.png)

然后让 Gemini 功能对你开放。

```csharp
"is_glic_eligible": true
```

如果找不到这些字段，直接在文件开头的大括号后面添加就行。

保存，重启 Chrome。

这个方法参考了 GitHub 上的开源项目 `https://github.com/lcandy2/enable-chrome-ai` ，感兴趣可以去看看，里面有一键脚本可以自动完成上面这些操作。

别忘了给作者点个 Star。

---

### 05｜检查谷歌账号的关联地区

Chrome 的配置文件只是一半。

谷歌账号本身也有一个「关联地区」的概念。

如果你的账号地区不是美国，某些功能依然可能受限（比如 Gemini）。

怎么查？

访问 `policies.google.com/terms` ，页面底部会显示当前关联的地区。

![](https://i-blog.csdnimg.cn/img_convert/261160c6462b30af6a8752e7fe4c668f.png)

如果不是美国，可以申请更改。

访问 `policies.google.com/country-association-form` ，地区选择 US，原因选择「Other reason」，说明你需要使用美国地区的服务。

审核通过后，谷歌会在几天内邮件回复。

还有个更快的办法。

去 `pay.google.com` 添加一个美国地址的付款资料。

谷歌会根据付款资料判断你的归属地区。

即使添加失败，账号区域往往也会变成美国。

---

### 06｜其他

官方文档明确要求 Chrome 语言是 English (United States)。

打开 Chrome 设置，搜索 Language，把英语调到第一位。

更新到最新版。

设置 -> 关于 Chrome -> 检查更新。

---

总结一下。

先试 `chrome://flags` 里启用 `glic` ，能用就完事了。

不行的话，改 `Local State` 配置文件，把 `variations_country` 和 `variations_permanent_consistency_country` 设置成 `us` ， `is_glic_eligible` 设置成 `true` 。

最后别忘了检查谷歌账号的关联地区。