---
title: "Animate使用"
date: 2019-06-08T20:23:29+08:00
categories:
- angular
- animate
tags:
- angular
- animate
keywords:
- animate
#thumbnailImage: //example.com/image.jpg
---

本教程将讲解如何在angular8.x动画模块。Angular动画是一个可选的服务，在它自己的`@angular/animations`包 和 `@angular/platform-browser`中。

<!--more-->

<!--toc-->

1.  导入包

   ```
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
   
   @NgModule({
     imports: [
       BrowserModule,
       BrowserAnimationsModule
     ],
     declarations: [ ],
     bootstrap: [ ]
   })
   export class AppModule { }
   ```

2. 把动画功能函数导入组件文件

   ```
   import { Component, HostBinding } from '@angular/core';
   import {
     trigger,
     state,
     style,
     animate,
     transition,
     // ...
   } from '@angular/animations';
   
   @Component({
     selector: 'app-root',
     templateUrl: 'app.component.html',
     styleUrls: ['app.component.css'],
     animations: [
       // animation triggers go here
     ]
   })
   ```

   

