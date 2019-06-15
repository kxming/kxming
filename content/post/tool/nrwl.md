---
title: "Nrwl"
date: 2019-05-30T19:10:12+08:00
categories:
- Tool
- Angular
- Nrwl
tags:
- tool
- Nrwl
keywords:
- tech
---

Nrwl是angular-cli的超集，扩展了angular-cli原理图与构建器，可以实现monorepo风格的开发。你可以在工作区中同时使用angular与react构建使用不同框架的前端应用程序，同时可以包含nodejs后台应用程序实现在同一存储库中开发全栈应用。

<!--more-->

<!--toc-->

### 安装

`npm install -g  @nrwl/schematics`

### 创建应用程序	

##### 创建工作区

`npx`使用请看[阮一峰教程](<http://www.ruanyifeng.com/blog/2019/02/npx.html>)。

`npx  --ignore-existing create-nx-workspace myorg`

创建过程中可以选择工作区类型:

```
  empty             [an empty workspace]
  angular           [a workspace with a single Angular application]
  angular-ivy       [a workspace with a single Angular application built using Ivy]
  react             [a workspace with a single React application]
  web components    [a workspace with a single app built using web components]
  full-stack        [a workspace with a full stack application (NestJS + Angular Ivy)]
```

创建完成后`myorg`目录中的内容为：

```
myorg/
├── apps/
├── libs/
├── tools/
├── nx.json
├── angular.json
├── package.json
├── tsconfig.json
├── tslint.json
└── README.md
```

##### 创建angular应用程序

首先添加创建angular应用程序的功能：

`ng add @nrwl/angular`

也可添加不同功能的应用程序：

```
ng add @nrwl/angular # Adds Angular capabilities
ng add @nrwl/react # Adds React capabilities
ng add @nrwl/nest # Adds Nest capabilities
ng add @nrwl/express # Adds Express capabilities
ng add @nrwl/web # Adds Web capabilities
ng add @nrwl/node # Adds Node capabilities
```

然后创建angular应用程序：

`ng g @nrwl/angular:application todos`

创建完成后目录内容为：

```
myorg/
├── apps/
│   ├── todos/
│   │   ├── src/
│   │   │   ├── app/
│   │   │   ├── assets/
│   │   │   ├── environments/
│   │   │   ├── favicon.ico
│   │   │   ├── index.html
│   │   │   ├── main.ts
│   │   │   ├── polyfills.ts
│   │   │   ├── styles.scss
│   │   │   └── test.ts
│   │   ├── browserslist
│   │   ├── jest.conf.js
│   │   ├── tsconfig.app.json
│   │   ├── tsconfig.json
│   │   ├── tsconfig.spec.json
│   │   └── tslint.json
│   └── todos-e2e/
│       ├── src/
│       │   ├── fixtures/
│       │   │   └── example.json
│       │   ├── integration/
│       │   │   └── app.spec.ts
│       │   ├── plugins/
│       │   │   └── index.ts
│       │   └── support/
│       │       ├── app.po.ts
│       │       ├── commands.ts
│       │       └── index.ts
│       ├── cypress.json
│       ├── tsconfig.e2e.json
│       ├── tsconfig.json
│       └── tslint.json
├── libs/
├── tools/
├── angular.json
├── nx.json
├── package.json
├── tsconfig.json
├── tslint.json
└── README.md
```

##### 运行应用程序

```
ng serve todos
```

##### 创建react应用程序

首先添加创建react应用程序的功能：

`ng add @nrwl/react`

然后创建react应用程序：

`ng g @nrwl/react:app reactapp`

创建完成后目录内容为：

```
happynrwl/
├── apps/
│   ├── todos/
│   ├── todos-e2e/
│   ├── reactapp/
│   │   ├── src/
│   │   │   ├── app/
│   │   │   │   ├── app.css
│   │   │   │   ├── app.spec.tsx
│   │   │   │   └── app.tsx
│   │   │   ├── assets/
│   │   │   ├── environments/
│   │   │   ├── favicon.ico
│   │   │   ├── index.html
│   │   │   ├── main.ts
│   │   │   ├── polyfills.ts
│   │   │   ├── styles.scss
│   │   │   └── test.ts
│   │   ├── browserslist
│   │   ├── jest.conf.js
│   │   ├── tsconfig.app.json
│   │   ├── tsconfig.json
│   │   ├── tsconfig.spec.json
│   │   └── tslint.json
│   └── reactapp-e2e/
│       ├── src/
│       │   ├── integrations/
│       │   │   └── app.spec.ts
│       │   ├── fixtures/
│       │   ├── plugins/
│       │   └── support/
│       ├── cypress.json
│       ├── tsconfig.e2e.json
│       └── tslint.json
├── libs/
├── README.md
├── angular.json
├── nx.json
├── package.json
├── tools/
├── tsconfig.json
└── tslint.json
```

运行应用程序

`ng serve reactapp`

### 添加node应用程序

##### 添加nest.js的功能

`ng add @nrwl/nest`

##### 添加express.js的功能

`ng add @nrwl/express`

##### 添加node.js的功能

`ng add @nrwl/node`

##### 创建nest应用程序

`ng g @nrwl/nest:app api --frontendProject=todos`

`--frontendProject=todos`将为angular应用程序与api创建代理配置。

创建完成后目录内容为：

```
myorg/
├── apps/
│   ├── todos/
│   ├── todos-e2e/
│   └── api/
│       ├── jest.conf.js
│       ├── proxy.conf.json
│       ├── src/
│       │   ├── app/
│       │   │   ├── app.controller.ts
│       │   │   ├── app.controller.spec.ts
│       │   │   ├── app.module.ts
│       │   │   ├── app.service.ts
│       │   │   └── app.service.spec.ts
│       │   ├── assets/
│       │   ├── environments/
│       │   │   ├── environment.ts
│       │   │   └── environment.prod.ts
│       │   └── main.ts
│       ├── tsconfig.app.json
│       ├── tsconfig.json
│       ├── tsconfig.spec.json
│       └── tslint.json
├── libs/
├── nx.json
├── package.json
├── tools/
├── tsconfig.json
└── tslint.json
```

##### 运行应用程序

`ng serve api`

### 创建共享代码库

##### 创建angular与nest公共接口

`ng g @nrwl/workspace:lib data`

创建完成后目录内容为：

```
myorg/
├── apps/
│   ├── todos/
│   ├── todos-e2e/
│   └── api/
├── libs/
│   └── data/
│       ├── jest.conf.js
│       ├── src/
│       │   ├── lib/
│       │   │   └── data.ts
│       │   └── index.ts
│       ├── tsconfig.app.json
│       ├── tsconfig.json
│       ├── tsconfig.spec.json
│       └── tslint.json
├── nx.json
├── package.json
├── tools/
├── tsconfig.json
└── tslint.json
```

在data.ts定义接口：

```
export interface Todo {
  title: string;
}
```

在angular中使用：

```
import { Todo } from '@myorg/data';
```

##### 创建angular组件库

`ng g @nrwl/angular:lib ui`

创建完成后目录内容为：

````
myorg/
├── apps/
│   ├── todos/
│   ├── todos-e2e/
│   └── api/
├── libs/
│   ├── data/
│   └── ui/
│       ├── jest.conf.js
│       ├── src/
│       │   ├── lib/
│       │   │   ├── ui.module.spec.ts
│       │   │   └── ui.module.ts
│       │   └── index.ts
│       ├── tsconfig.app.json
│       ├── tsconfig.json
│       ├── tsconfig.spec.json
│       └── tslint.json
├── nx.json
├── package.json
├── tools/
├── tsconfig.json
└── tslint.json
````

添加组件

`ng g component todos --project=ui --export`

注册`CUSTOM_ELEMENTS_SCHEMA`模式，这将告诉Angular编译器在组件模板中看到非标准元素标签时不会出错。

```
//app.module
import { NgModule, CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';

@NgModule({
  ...
  schemas: [CUSTOM_ELEMENTS_SCHEMA],
  ...
})
export class AppModule {}
```

使用方法同angular-cli创建的lib相同。

##### 创建angular与react共享组件库

`ng g @nrwl/workspace:lib ui`

```
myorg/
├── apps/
│   ├── todos/
│   ├── todos-e2e/
│   ├── reactapp/
│   └── reactapp-e2e/
├── libs/
│   └── ui
│       ├── src/
│       │   ├── lib/
│       │   └── index.ts
│       ├── jest.conf.js
│       ├── tsconfig.lib.json
│       ├── tsconfig.json
│       ├── tsconfig.spec.json
│       └── tslint.json
├── README.md
├── angular.json
├── nx.json
├── package.json
├── tools/
├── tsconfig.json
└── tslint.json
```

在lib下面创建greeting.element.ts组件：

```
export class GreetingElement extends HTMLElement {
  public static observedAttributes = ['title'];

  attributeChangedCallback() {
    this.innerHTML = `<h1>Welcome to ${this.title}!</h1>`;
  }
}

customElements.define('happynrwl-greeting', GreetingElement);
```

并在index.js导出

```
export * from './lib/greeting.element';
```

###### 在angular中使用

在main.js导入

```
import '@myorg/ui'; // <-- the new library
```

在app.module注册`CUSTOM_ELEMENTS_SCHEMA`,然后就可以在angular中使用。

###### 在react中使用

在main.tsx中导入：

```
import '@happynrwl/ui';
```

在`src`下面添加`intrinsic.d.ts`文件，创建如下内容：

```
declare namespace JSX {
  interface IntrinsicElements {
    [elemName: string]: any;
  }
}
```

在app.tsx中使用：

```
import * as React from 'react';
import { Component } from 'react';

import './app.css';

export class App extends Component {
  render() {
    const title = 'reactapp';
    return (
      ...
      <happynrwl-greeting title={title} />
      ...
    );
  }
}
```



### 创建项目依赖图

Nx工作区可以包含几十个应用程序与库，随着代码库的增长，可以使用`npm run dep-graph`命令在浏览器中输出一个工作区依赖图。

