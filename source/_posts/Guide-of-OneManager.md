---
title: 如何优雅的使用OneManager
author: MCSeekeri
tags:
  - 教程
  - 网盘
categories:
  - 技术
description: 
abbrlink: Guide-of-OneManager
date: 2020-08-19 20:48:40
updated: 2021-05-02 17:21:00
---

鉴于我在OneManager群里当客服当的快吐了,而且逸笙前辈又死活不更新README,所以我专门抽出时间来写一个完全版本的OneManager教程。

<!-- more -->

## 原材料准备
- 稳定的互联网接入
- 一台智能设备(电脑手机均可)
- 有科学上网的工具
- 好使的脑子

## 找到官方Repo
就目前来讲,OneManager在传播的过程中各大博客二次打包/Fork的简直不成样子了,所以经常有人用着旧版软件来咨询我们问题,殊不知这个Bug已经修复了大约114514年了（大嘘
![暴躁内谁](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.3/ysun/7.png)
{% note warning, 切记！OneManager只在Github上更新，除此之外任何地方的代码可用性都不做保证！ %}
唯一官方指定Repo[在此](https://github.com/qkqpttgf/OneManager-php),别走丢了。
![Repo截图，存档于2020.8.19](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Github.png)
下文我就把OneManager简称OM了啊。

## 选择你的平台
因为逸笙前辈{% del 不想被我们骂万年不更新 %}为了增加OM的平台兼容性,所以兼容了一大波网络服务,算是各有优缺点罢,下面我整理了一下,你自己看着选。
### [Heroku](https://heroku.com/) 
{% checkbox plus green checked, 部署最简单 真正一键式 %}
{% checkbox plus green checked, 使用无需付费 %}
{% checkbox minus red checked, 配置过程需要科学上网 %}
{% checkbox minus red checked, 绑定域名需要信用卡(可通过反向代理绕过) %}
### [腾讯云函数](https://cloud.tencent.com/product/scf)
{% checkbox plus green checked, 访问速度快 %}
{% checkbox plus green checked, 自选地点丰富 %}
{% checkbox minus red checked, 按量付费，如果没做好反DDCC很容易倾家荡产 %}
{% checkbox minus red checked, 绑定域名需要经过备案 %}
{% checkbox minus red checked, 环境变量大小有限，理论上最多只能添加四个盘 %}
### [华为函数工作流](https://console.huaweicloud.com/functiongraph)
{% checkbox plus green checked, 程序不部署在中国大陆时绑定域名无需备案 %}
{% checkbox minus red checked, 环境变量大小有限，理论上最多只能添加两个盘 %}
其余同腾讯云函数
### [阿里函数计算](https://fc.console.aliyun.com)
{% checkbox plus green checked, 环境变量大小无限制 %}
其余同华为函数工作流
### [百度云函数计算](https://console.bce.baidu.com/cfc/#/cfc/functions)
{% checkbox plus green checked, 有免费额度，完全足够使用 %}
其余同腾讯云函数
### 自家VPS或虚拟空间
{% checkbox plus green checked, 你说呢 %}
{% checkbox minus red checked, 你说呢 %}

## 开始部署
总之,在选好平台之后就该开始安装程序力！
因为OM不管部署在哪里,安装过程都差不多,所以这里先分开讲不同平台怎么部署{% del ，之后糊弄一下安装过程就可以啦 %}
![名   言   警   句](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.3/ysun/2.png)
{% del 点点点就完了有啥难度 %}
### Heroku部署
打开Repo你应该能看到那个裂了的图,点那个Deploy就成了。
![没梯子就是这么可怜](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Heroku.png)
然后会跳转到Heroku,记得带上梯子和脑子,安装之前需要注册账号,这里我略过不讲。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.3/ysun/34.png)
然后你就会看到配置页面,起名,选地点,点Deploy app,搞定!
![我们是OM,不是隔壁OneIndex](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Heroku-Deploy.png)
然后就是点点点。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Install.png)
![申请了填进去就好](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Heroku-APIKey.png)
### 腾讯云函数部署
点击Repo里那个又大又绿的下载按钮。
![点就完了](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Download.png)
然后选择"Download ZIP",当然你能Clone也行。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Download-ZIP.png)
下载下来之后解压,然后点开目录,Ctrl+A选择所有文件,打包。
{% span red, 没这个过程你程序大概率部署失败，别来找我售后 %}
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.3/ysun/44.png)
然后奔向[腾讯云函数官网](https://cloud.tencent.com/product/scf)
注册账号不解释。
左上角选好地点,然后点击新建函数。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF.png)
推荐空白模板,但偏要选另外一个我也没办法,反正不管是啥都要被干掉换成OM的代码。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.3/ysun/16.png)
上传你二次打包的压缩包,不解释。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF2.png)
左边点触发管理,新建触发,按照图片设置。
{% note warning, 务必勾选"启用集成响应" %}
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF-API.png)
然后去安装程序。记得新建SecretId和SecretKey。
![反正不管选哪个都是要花点钱的](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF-Install.png)
我建议你新建个只能访问SCF和API的账户,安全第一。
新建访问密钥的那个页面侧边栏,点用户,新建用户
![务必记得开编程访问](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF-NewUser.png)
然后把SecretId和SecretKey填回去,搞定。

如果你需要自定义域名,那就要回到API设置那个地方,点开"管理API",点编辑,然后把路径删到只剩下个斜杠。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF-API-Config.png)
一路下一步,之后回到"服务信息"那里,把API发布一下。
![光看气势你们已经输了](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF-API2.png)
"自定义域名"那里新建域名。
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/SCF-Domain.png)
如果需要SSL,可以用Cloudflare的源服务器证书,也可以去腾讯申请个TrustAsia证书。
## 程序安装
之后就是枯燥无味的安装了,因为在几乎所有平台上OM表现都几乎一致
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Install.png)
总之跟着步骤来,该添加API的添加API,该复制的复制。
## 配置详解
![](https://cdn.jsdelivr.net/npm/mcseekeri@1.2.4/post/Guide-of-OneManager/Full-Setting.png)
嗯……因为这里很多的说明都是祖传代码了,可能不易理解,所以我简单翻译下。

### 平台变量
- adminloginpage

隐藏登录按钮,只能通过访问[你的域名]/?[设置的内容]来打开管理界面
> 示例: login
> 访问:https://example.com/?login

- autoJumpFirstDisk

添加多盘时加一个跳转,不设置的话访问根目录时会让你选择哪个盘,设为1会自动打开第一个盘。

- background

背景图片,建议使用[去不图床](https://7bu.top),速度和稳定性都有保证,上传完把链接丢过来
> 示例: https://cdn.jsdelivr.net/npm/mcseekeri@1.2.3/img/FutureGadgetLab.webp

- backgroundm

同上,只不过是给手机准备的。

- customCss

自定义CSS格式,一般用户直接无视就好

- customScript

在每个页面里插入JS脚本,可以放统计代码啥的。
因为屑逸笙没写多行处理,所以你直接在别的地方写完复制到这就行
> 示例: `<script>   window.ga_tid = 'UA-104605102-3';   (function() {     var dga = document.createElement("script");     dga.src = "https://rmt.dogedoge.com/fetch/public/ga.js";     var s = document.getElementsByTagName("script")[0];     s.parentNode.insertBefore(dga, s);   })(); </script>`

{% note warning, 部分主题并没有对这个选项做兼容,所以我个人推荐使用renexmoe主题 %}

- passfile

保存密码的文件名…不是密码！
更不是全站加密！
譬如罢,你把这个设置成`.password`,然后去加密某个目录,OM就会在你的OneDrive里创建一个叫`.password`的文件,里面是这个文件夹的密码。
所以设置好了不要轻易改,一改你原本的密码文件就可以看作失效了（
而且为了兼容性,我个人建议设置为`.password`就好,因为诸如GDIndex,GoIndex之类的目录程序都把这个作为密码文件名。

- theme

选renexmoe.html！

186记得给我广告费。

### 盘内变量

- domain_path

不同的域名将不同的目录作为根目录…概念有点绕…
如果是Heroku部署且没绑卡,这个变量毫无作用…其他云函数平台可以
> 示例: example.com:/默认/|bangumi.example.com:/番剧/|movie.example.com:/电影/|nsfw.example.com:/小姐姐/

- downloadencrypt

简单说,就是是否可以无需密码下载加密目录里的文件。

比如你有个加密文件夹"NSFW",里面有个文件叫186526.mkv。
别人打开目录是啥也看不见的,毕竟他们没密码,但是你可以给他们`https://example.com/NSFW/186526.mkv`这个链接让他们下载目录里的文件。
近似于*nix系统中对目录rwx与-wx的区别

- guestup_path

把某个文件夹设置成游客上传,文件夹内容不会展示,游客上传文件后可以拿到链接。
顺带一提文件会被强制重命名为文件的md5
{% note warning, 不要想着提建议说删掉自动重命名,我2年前就提过多次,屑逸笙就是不改（叹气 %}
> 示例: /NSFW/186526/

- public_path

设置某个目录为全站根目录。
> 示例:/NSFW

> 没有提到的配置项大多数不需要说明,或者一般用户用不着（
## 特殊玩法
