---
title: "Storybook"
date: 2019-05-30T19:07:49+08:00
categories:
- Tool
- Storybook
tags:
- Tool
- Storybook
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---
Storybook是一个UI组件开发环境，它允许你浏览组件库，查看每个组件的不同状态，以及交互式开发和测试组件。Storybook运行在主应用程序之外，因此用户可以独立开发UI组件，而无需担心应用程序的特定依赖关系和需求。并且提供了灵活的API以及各种插件，还可以在http服务构建构建静态网站。

Storybook支持Angular、React、Vue、ReactNative等组件。

<!--more-->

### 示例

* [Demo of React Dates](http://airbnb.io/react-dates/) - [source](https://github.com/airbnb/react-dates)
* [Demo of React Native Web](http://necolas.github.io/react-native-web/storybook/) - [source](https://github.com/necolas/react-native-web)

### 安装

```
npm install -g @storybook/cli
sb --version
```

### 使用

1. Angular

   ```
   cd project
   sb init
   ```



2. React

   ```
   cd project
   sb init
   ```



3. Vue

   ```
   cd project
   sb init
   ```



4. HTML

   * 自动设置

     ```
     cd project
     sb init --type html
     npm run storybook
     ```

   * 手动设置

     * 添加依赖

       ```
       cd project
       npm install @storybook/html babel-loader @babel/core --save-dev
       ```

     * 添加npm脚本

       ```javascript
       {
       	"scripts": {
       		"storybook": "start-storybook",
       	}
       }
       ```

     * 创建配置文件

       ```javascript
       import { configure } from '@storybook/html';

       function loadStories() {
         require('../stories/index.js');
       }

       configure(loadStories, module);
       ```

       创建`.storybook/config.js`。

     * 编写stories

       在`.storybook/index.js`中编写下面代码：

       ```javascript
       import { storiesOf } from '@storybook/html';

       storiesOf('Button', module)
         .add('with text', () => '<button class="btn">Hello World</button>')
         .add('with emoji', () => {
           const button = document.createElement('button');
           button.innerText = '😀 😎 👍 💯';
           return button;
         });
       ```



