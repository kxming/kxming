---
title: "Hugo创建个人博客指南"
date: 2019-05-26T17:44:53+08:00
categories:
- blog
tags:
- blog
- Hugo
keywords:
- hugo
- blog
---

本博客使用[Hugo](https://gohugo.io/)静态页面生成引擎，使用的主题是[tranquilpeak](https://tranquilpeak.kakawait.com/)，使用的评论系统为[Valine](https://valine.js.org/)。写这篇文章的目的是详细介绍个人博客创建指南。
<!--more-->


### 准备工作
  * Git、Golang环境
  * [GitHub](https://github.com)账户或者[Gitee](https://gitee.com/)账户（使用免费的pages服务搭建博客）
  * [Wordpress](https://wordpress.com)账户（提供个人头像）
  * [LeanCloud](https://leancloud.cn)账户（管理评论数据）

###### 安装Git、golang、创建GitHub、码云（gitee）账户过程略过

###### 安装Hugo

  本篇博客安装使用Windows系统，其他系统请看[Hugo](https://gohugo.io/)官网。

* 直接在GitHub下载最新版本[zip](https://github.com/gohugoio/hugo/releases)包，并添加到环境变量。
* 或者使用choco在命令行下载`choco install hugo`

安装成功后在命令行输入`hugo version`显示下图，说明安装成功。

`Hugo Static Site Generator v0.55.6-A5D4C82D windows/amd64 BuildDate: 2019-05-18T07:57:00Z`

###### 创建并配置站博客

1. 创建博客
    `hugo new site myblog`
2. 下载[hugo-tranquilpeak-theme](https://tranquilpeak.kakawait.com/)主题
    ```
    cd myblog/themes
    git clone https://github.com/kakawait/hugo-tranquilpeak-theme.git tranquilpeak
    ```
3. 修改config.toml配置文件
    复制`themes/tranquilpeak/exampleSite`文件夹下config.toml到`myblog`覆盖原有config.toml。
    在GitHub查看tranquilpeak主题[配置项](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md)
    以下为本博客配置文件
    ```
    baseURL = "https://your_name.github.io/your_name/"
    # Tips: 必须配置，否则上传的博客在GitHub Pages无法找到css文件，不产生样式
    languageCode = "en-us"
    defaultContentLanguage = "zh-cn"
    # Tips: 配置中文
    title = "KXMing"
    # Tips: 博客名称
    theme = "tranquilpeak"
    # Tips: 配置主题
    disqusShortname = "valine"
    # Tips: 评论系统
    paginate = 10
    # Tips: 每个页面显示的文章数
    canonifyurls = true
    publishDir = "docs"
    # Tips: 生成静态博客到docs文件夹，部署在GitHub Pages上时，一次性部署博客源码与发布博客

    [permalinks]
      post = "/:year/:month/:slug/"

    [taxonomies]
      tag = "tags"
      category = "categories"
      archive = "archives"
    # Tips: 定义的博客分类与逻辑关系

    [author]
      name = "your_name"
      # Tips: 博客侧边栏名字
      bio = "前端开发"
      # Tips: 博客侧边栏个人简介
      job = "Front-end"
      # Tips: 博客侧边栏职业
      location = "深圳"
      # Tips: 博客个人资料页面地址
      gravatarEmail = "964579219@qq.com"
      # Tips: 博客个人头像，取自WordPress头像

    # Tips: 定义的侧边栏菜单，icon取自Font-awesome
    [[menu.main]]
      weight = 1
      identifier = "首页"
      name = "首页"
      pre = "<i class=\"sidebar-button-icon fa fa-lg fa-home\"></i>"
      url = "/"
    ...
    [[menu.links]]
    ...
    [[menu.misc]]

    [params]
      dateFormat = "2006年1月2日"
      # Tips: 默认日期格式
      syntaxHighlighter = "highlight.js"
      # Tips: 语法高亮js库
      clearReading = true
      # Tips: 进入文章内容页面侧边栏菜单收起状态
      hierarchicalCategories = true
      sidebarBehavior = 2
      # Tips: 定义侧边栏状态（值为1-6，可自行测试显示状态）
      coverImage = "cover.jpg"
      imageGallery = true
      # Tips: 在有内容底部显示照片墙

      thumbnailImage = true
      # Tips: 列表页是否显示内容图片
      thumbnailImagePosition = "bottom"
      # Tips: 列表页显示内容图片在底部
      autoThumbnailImage = true

      favicon = "/favicon.ico"
      # Tips: 浏览器标签页本网站显示的图标，放置在static文件夹下

    [params.header.rightLink]
      class = ""
      icon = ""
      url = "/#about"
    # Tips: 是否显示页面头部右侧个人头像，及个人头像点击事件

    # 这里添加Valine评论系统的相关参数
    [params.valine]
      enable = true
      appId = 'your appid'
      appKey = 'your appkey'
      notify = false
      avatar = 'mm'
      placeholder = '说点什么吧...'
      visitor = true
    ```
4. 创建第一篇博客
    `hugo new post/first_blog.md`
    文件顶部设置，其余配置请参考[tranquilpeak](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md#writing-posts)
    ```
    title: "本篇博客名称"
    date: 2019-05-26T17:44:53+08:00
    categories:
    - 父类
    - 子类
    tags:
    - 标签
    keywords:
    - 关键字

    more标签上方的内容会在列表页显示内容简介
    <!--more-->
    toc标签会生成本篇文章的目录
    <!-- toc -->
    ```
    `hugo serve`
    在浏览器localhost:1313端口访问本地服务
5. 安装Valine评论系统

    > Valine - 一款快速、简洁且高效的无后端评论系统。

    安装教程参考[smslit](https://www.smslit.top/2018/07/08/hugo-valine/)

    修改主题文件

    打开themes/layouts/partials/post文件，将原有内容替换为valine评论代码
6. 部署GitHub Pages或者Gitee Pages

    在GitHub创建新项目，上传本项目代码，打开settings/options，选择GitHub Pages Source选项为master branch/docs folder，等待部署，成功后可在https://your_name.github.io/your_folder_name 查看创建的博客。

    在码云创建新项目，上传本项目代码或者导入GitHub本项目，打开服务/Gitee Pages，部署目录填写docs，等待部署，成功后可在https://your_name.gitee.io 查看创建的博客。

> 本博客内容为简单配置，更多博客主题、评论配置可在各自官网查看。
