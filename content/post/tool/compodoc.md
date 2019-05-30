---
title: "Compodoc"
date: 2019-05-26T23:23:53+08:00
categories:
- Tool
- Angular
- Compodoc
tags:
- Tool
- Angular
keywords:
- compodoc
---
Compodoc是Angular应用程序的一个文档工具。它生成应用程序的静态文档。可用于Angular、Nestjs、Stencil框架，包含8中内置主题，4种语言选项。
<!--more-->


### 示例

https://compodoc.github.io/compodoc-demo-todomvc-angular/overview.html

### 下载

`npm install -g @compodoc/compodoc`

`npm install --save-dev @compodoc/compodoc`



### 运行

在package.json中定义一个任务。

```nodejs
"scripts": {
  "compodoc": "npx compodoc -p src/tsconfig.app.json"
}
```

`npm run compodoc`

### 用法

`compodoc <src>  [option]`

下面列出常用的配置属性：

| 属性                   | 说明                                                         |
| :--------------------- | ------------------------------------------------------------ |
| -c, --config [config]  | .compodocrc, .compodocrc.json, .compodocrc.yaml 或者在 package.json中的compodoc属性 |
| -p, --tsconfig [config | tsconfig.json文件                                            |
| -d, --output [folder]  | 输出目录                                                     |
| -y, --extTheme [file]  | 外部主题文件                                                 |
| -n, --name [name]      | 文档名称                                                     |
| -o, --open             | 打开生成的文档                                               |
| -s, --serve            | 在http://localhost:8080/自动打开文档                         |
| -r, --port [port       | 更改服务端口                                                 |
| --language [language]  | 指定文档语言(en-US, fr-FR, zh-CN, pt-BR) (default: en-US)    |
| --theme [theme]        | 选择一个主题(gitbook-默认，laravel, original, material, postmark, readthedocs, stripe, vagrant) |
| --hideGenerator        | 生成的文档菜单栏底部隐藏compodoc logo                        |

全部属性请访问[compodoc](<https://compodoc.app/guides/usage.html>).

### 配置文件

你可以在项目目录创建一个 **.compodocrc**, **.compodocrc.json**, **.compodocrc.yaml** 或者在 package.json中定义**compodoc**属性。

```
{
   ...
   "doc": "npx compodoc -p src/tsconfig.app.json -n \"My app documentation\""
   ...
}
```

`npm run doc`

### 文档主要内容

- `Overview` 项目主要内容统计概览。图形化展示主要模块、组件、指令等
- `README` 由项目根目录 `README.MD` 生成
- `Dependencies` 项目第三方依赖列表
- `Modules` 所有模块的列表。生成有模块依赖图列表
- `Components` 独立组件
- `Directives` 独立指令
- `Classes` 独立类列表
- `Injectables` 使用 Injectables 装饰器修饰的独立类列表
- `Interfaces` 所有接口定义列表
- `Pipes` 管道列表
- `Routes` 路由树图。路由定义需指定类型为 `Routes` (从 `@angular/router` 导入)
- `Miscellaneous` 其他杂项内容集合。根据这里的内容，可以分析分散的重复定义的内容，不合理的杂项定义等
- `Documentation coverage` 文档覆盖率信息

### 主题

默认（Gitbook）

![gitbook](https://kxming.github.io/kxming/angular/tool/theme-gitbook.png)

Material Design

![material](https://kxming.github.io/kxming/angular/tool/theme-material.png)

Laravel

![laravel](https://kxming.github.io/kxming/angular/tool/theme-laravel.png)

Readthedocs

![readthedocs](https://kxming.github.io/kxming/angular/tool/theme-readthedocs.png)

Stripe

![stripe](https://kxming.github.io/kxming/angular/tool/theme-stripe.png)

Vagrant

![vagrant](https://kxming.github.io/kxming/angular/tool/theme-vagrant.png)

Postmark

![postmark](https://kxming.github.io/kxming/angular/tool/theme-postmark.png)

Original

![original](https://kxming.github.io/kxming/angular/tool/theme-original.png)