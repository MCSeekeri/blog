---
title: 如何优雅的使用OneManager
author: MCSeekeri
pin: false
toc: true
tags:
  - 教程
  - 网盘
categories:
  - 技术
description: 教你如何配置OneManager并且避开大多数坑
abbrlink: Guide-of-OneManager
date: 2020-08-19 20:48:40
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
![暴躁内谁](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/ysun/7.png)
{% note warning, 切记！OneManager只在Github上更新，除此之外任何地方的代码可用性都不做保证！ %}
唯一官方指定Repo[在此](https://github.com/qkqpttgf/OneManager-php),别走丢了。
![Repo截图，存档于2020.8.19](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Github.png)
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
![名   言   警   句](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/ysun/2.png)
{% del 点点点就完了有啥难度 %}
### Heroku部署
打开Repo你应该能看到那个裂了的图,点那个Deploy就成了。
![没梯子就是这么可怜](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Heroku.png)
然后会跳转到Heroku,记得带上梯子和脑子,安装之前需要注册账号,这里我略过不讲。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/ysun/34.png)
然后你就会看到配置页面,起名,选地点,点Deploy app,搞定!
![我们是OM,不是隔壁OneIndex](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Heroku-Deploy.png)
然后就是点点点。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Install.png)
![申请了填进去就好](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Heroku-APIKey.png)
### 腾讯云函数部署
点击Repo里那个又大又绿的下载按钮。
![点就完了](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Download.png)
然后选择"Download ZIP",当然你能Clone也行。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/Download-ZIP.png)
下载下来之后解压,然后点开目录,Ctrl+A选择所有文件,打包。
{% span red, 没这个过程你程序大概率部署失败，别来找我售后 %}
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/ysun/44.png)
然后奔向[腾讯云函数官网](https://cloud.tencent.com/product/scf)
注册账号不解释。
左上角选好地点,然后点击新建函数。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF.png)
推荐空白模板,但偏要选另外一个我也没办法,反正不管是啥都要被干掉换成OM的代码。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/ysun/16.png)
上传你二次打包的压缩包,不解释。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF2.png)
左边点触发管理,新建触发,按照图片设置。
{% note warning, 务必勾选"启用集成响应" %}
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF-API.png)
然后去安装程序。记得新建SecretId和SecretKey。
![反正不管选哪个都是要花点钱的](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF-Install.png)
我建议你新建个只能访问SCF和API的账户,安全第一。
新建访问密钥的那个页面侧边栏,点用户,新建用户
![务必记得开编程访问](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF-NewUser.png)
然后把SecretId和SecretKey填回去,搞定。

如果你需要自定义域名,那就要回到API设置那个地方,点开"管理API",点编辑,然后把路径删到只剩下个斜杠。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF-API-Config.png)
一路下一步,之后回到"服务信息"那里,把API发布一下。
![光看气势你们已经输了](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF-API2.png)
"自定义域名"那里新建域名。
![](https://cdn.jsdelivr.net/gh/MCSeekeri/cdn@master/posts/Guide-of-OneManager/SCF-Domain.png)
如果需要SSL,可以用Cloudflare的源服务器证书,也可以去腾讯申请个TrustAsia证书。

## 程序安装
## 配置详解
## 特殊玩法
