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

   * 自动设置
   
     ```
     cd angular-project
     sb init
     ```
   
   * 手动设置
   
     - 添加依赖
   
       ```
       cd react-project
       npm install --save-dev @storybook/angular babel-loader @babel/core
       ```
   
       
   
     - 添加npm脚本
   
       ```
       {
         "scripts": {
           "storybook": "start-storybook"
         }
       }
       ```
   
       
   
     - 创建配置文件
   
       ```
       // 创建.storybook/config.js
       import { configure } from '@storybook/angular';
       
       function loadStories() {
         require('../stories/index.js');
         // You can require as many stories as you need.
       }
       
       configure(loadStories, module);
       ```
   
     - Storybook Typescript配置
   
       ```
       // 在.storybook/tsconfig.json添加如下内容：
       {
         "extends": "../tsconfig.json",
         "exclude": [
           "../src/test.ts",
           "../src/**/*.spec.ts",
           "../projects/**/*.spec.ts"
         ],
         "include": [
           "../src/**/*",
           "../projects/**/*"
         ]
       }
       ```
   
       
   
     - 编写stories
   
       ```
       // 在..storybook/index.js中编写下面代码：
       import { storiesOf } from '@storybook/angular';
       import { Button } from '@storybook/angular/demo';
       
       storiesOf('My Button', module)
        .add('with text', () => ({
           component: Button,
           props: {
             text: 'Hello Button',
           },
         }))
         .add('with emoji', () => ({
           component: Button,
           props: {
             text: '😀 😎 👍 💯',
           },
         }));
       ```
   
       
   
     - 运行
   
       `npm run storybook`
   
2. React

   * 自动设置

     ```
     cd react-project
     sb init --type react
     ```

   * 手动设置

     * 添加依赖

       ````
       cd react-project
       npm install --save-dev @storybook/react babel-loader @babel/core
       ````

       

     * 添加npm脚本

       ```
       {
         "scripts": {
           "storybook": "start-storybook"
         }
       }
       ```

       

     * 创建配置文件

       ```
       // 创建.storybook/config.js
       import { configure } from '@storybook/react';
       
       function loadStories() {
         require('../stories/index.js');
         // You can require as many stories as you need.
       }
       
       configure(loadStories, module);
       ```

       

     * 编写stories

       ```
       // 在..storybook/index.js中编写下面代码：
       import React from 'react';
       import { storiesOf } from '@storybook/react';
       import { Button } from '@storybook/react/demo';
       
       storiesOf('Button', module)
         .add('with text', () => (
           <Button>Hello Button</Button>
         ))
         .add('with emoji', () => (
           <Button><span role="img" aria-label="so cool">😀 😎 👍 💯</span></Button>
         ));   
       ```

       

     * 运行

       `npm run storybook`



3. Vue

   * 自动设置
   
     ```
     cd vue-project
     sb init --type vue
     ```
   
     
   
   * 手动设置
   
     - 添加依赖
   
       ```
       cd react-project
       npm install --save-dev @storybook/vue vue-loader vue-template-compiler @babel/core babel-loader babel-preset-vue
       ```
   
       
   
     - 添加npm脚本
   
       ```
       {
         "scripts": {
           "storybook": "start-storybook"
         }
       }
       ```
   
       
   
     - 创建配置文件
   
       ```
       // 创建.storybook/config.js
       import { configure } from '@storybook/vue';
       
       function loadStories() {
         require('../stories/index.js');
         // You can require as many stories as you need.
       }
       
       configure(loadStories, module);
       ```
   
       
   
     - 编写stories
   
       ```
       // 在..storybook/index.js中编写下面代码：
       import Vue from 'vue';
       import { storiesOf } from '@storybook/vue';
       import MyButton from './Button.vue';
       
       storiesOf('Button', module)
         .add('with text', () => '<my-button>with text</my-button>')
         .add('with emoji', () => '<my-button>😀 😎 👍 💯</my-button>')
         .add('as a component', () => ({
           components: { MyButton },
           template: '<my-button :rounded="true">rounded</my-button>'
         }));
       ```
   
       
   
     - 运行
   
       `npm run storybook`



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
       // 创建.storybook/config.js。
       import { configure } from '@storybook/html';
       
  function loadStories() {
         require('../stories/index.js');
       }
  
       configure(loadStories, module);
  ```
     
* 编写stories
     
  
     
       ```javascript
  // 在..storybook/index.js中编写下面代码：
     import { storiesOf } from '@storybook/html';
       
       storiesOf('Button', module)
         .add('with text', () => '<button class="btn">Hello World</button>')
         .add('with emoji', () => {
           const button = document.createElement('button');
           button.innerText = '😀 😎 👍 💯';
           return button;
         });
       ```
       
     * 运行
     
       `npm run storybook`

### 配置

