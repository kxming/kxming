---
title: "Router使用"
date: 2019-06-08T14:56:31+08:00
categories:
- angular
- ng-router
tags:
- angular
- ng-router
keywords:
- angular
- router
#thumbnailImage: //example.com/image.jpg
---
本教程将讲解如何在angular8.x使用路由服务在页面之间导航。Angular路由器是一个可选的服务，在它自己的`@angular/router`包中。
<!--more-->

<!-- toc -->

1. 在src/index.html的<head>标签下添加一个<base>元素，目的是告诉路由器该如何合成导航用的URL。如果在创建项目的时候指定使用`ng new myapp --routing`命令会自动在index.html生成该元素。

2. 简单配置

   ```
   // app.module.ts
   import { RouterModule, Routes } from '@angular/router';
   
   const appRoutes: Routes = [
         {
           path: 'heroes', 
           component: HeroListComponent,
           data: { title: 'Heroes List' } // 路由相关任意信息,
           children: [{ // 子路由
               path: 'user/:name',
               component: User
           }]
         },
         { 
         	path: 'crisis-center', // 不能以斜杠“/”开头
         	component: CrisisListComponent，
         },
         { 
         	path: 'news', 
         	outlet:'let1'，// outlet匹配<router-outlet>标签name属性,默认值为primary
           component: NewsComponent
         },
         { 
         	path: 'crisis-center', // 不能以斜杠“/”开头
         	component: CrisisListComponent 
         },
         { 
         	path: 'hero/:id', // 路由参数
         	component: HeroDetailComponent 
         },
         { 
         	path: '', // URL为空时的默认路径
           redirectTo: '/heroes', // 重定向
           pathMatch: 'full/perfix' // full匹配剩下的,以perfix（变量）值开头匹配这个路由，
         },
         { 
         	path: '**', // URL不匹配时的路径
         	component: PageNotFoundComponent 
         },
         { 
         	matcher: mathFunc, // 自定义路径匹配，取代自定义策略path和pathMatch
         	component: CrisisListComponent，
         },
   ];
   export function mathFunc(
       segments: UrlSegment[], // [{path:string,params:[name: string]: string}]
       group: UrlSegmentGroup, // [UrlSegment[]同上,children:{key:UrlSegmentGroup}]
       route: Route) {
               return {
               	consumed: segments, //如果你的 route 还有 child 的话，这里要注意，只放入你所匹配到的范围，后面的交给 child 去判断.
               	posParams: { Id: segments[1] } // 传入 params, url matrix 等}:null
               	}
   	}
   @NgModule({
     imports: [
       RouterModule.forRoot( // 指定router单例服务
         appRoutes,
         { enableTracing: true } // 开发配置，在控制台输出导航生命周期事件
       )
     ],
     ...
   })
   export class AppModule { }
   ```

   

3. 出口

   ```
   <router-outlet name='left' //导航路由名称 (activate)='onActivate($event)' // 激活事件(deactivate)='onDeactivate($event)'// 取消激活事件></router-outlet>
   ```

   

4. 链接

   ```
   // 声明式
   <a routerLink="/heroes" routerLinkActive="active">Heroes</a>// 从根路由查找
   <a routerLink="./heroes" routerLinkActive="active">Heroes</a>// 从相对路由查找
   <a routerLink="../heroes" routerLinkActive="active">Heroes</a>// 从上一级路由查找
   <a [routerLink]="['/team', teamId, 'user', userName, {details: true}]">xxxHeroe</a> //路由参数，链接到/team/11/user/bob;details=true
   <a [routerLink]="['/user/bob']" [queryParams]="{debug: true}" fragment="education"></a> // 链接到/user/bob#education?debug=true
   <a [routerLink]="['/user/bob']" [queryParams]="{debug: true2}" queryParamsHandling="merge"></a> // 链接到/user/bob#education?debug=true?debug=true2
   <a [routerLink]="['/user/bob']" preserveQueryParams preserveFragment >xxxHeroe</a> // perserve保留当前查询参数
   <a [routerLink]="['/user/bob']" skipLocationChange>xxxHeroe</a> // 导航时不把新状态计入历史
   <a [routerLink]="['/user/bob']" replaceUrl>xxxHeroe</a> // 导航时不把当前状态计入历史
   <a [routerLink]="['/user/bob']" [state]="{tracingId: 123}">xxxHeroe</a> // 设置state保存在浏览器History.state属性中
   
   // 函数式
   this.router.navigate([路由参数],extras:{修改导航参数，上方所有导航策略})
   this.router.navigateByUrl(url:绝对路径,extras:{修改导航参数，上方所有导航策略})
   
   // 组件中获取路由信息
   import { Router, ActivatedRoute, ParamMap } from '@angular/router';
   constructor(
     private route: ActivatedRoute,
     private router: Router,
     private service: HeroService
   ) {
       ngOnInit() {
         this.route.url.subscribe(url => {[{path,parameters}]});
         this.route.params.subscribe(params => {路由参数：});
         this.route.queryParams.subscribe(queryParams => {路由参数？});
         this.route.fragment.subscribe(fragment => {路由参数#});
         this.route.data.subscribe(data => {路由data});
         this.route.paramMap.subscribe(paramMap => {矩阵参数（;）和查询参数（?）});
         this.route.queryParamMap.subscribe(queryParamMap => {});
         console.log（this.route.outlet）;// primary字符串
         console.log（this.route.routeConfig);
         { 
         	path: 'news', 
         	outlet:'let1'，
           component: NewsComponent
         }
         this.route.root/parent/firstChild/children/pathFormRoot返回当前路由的父子节点信息，获取方法同当前路由方法相同。
       }
   }
   
   //路由参数变化使用组件服用
   ngOnInit() {
     this.hero$ = this.route.paramMap.pipe(
       switchMap((params: ParamMap) =>
         this.service.getHero(params.get('id')))
     );
   }
   ```

   

5. 激活的路由状态

   ```
   <a routerLink="/user/bob" routerLinkActive="class1 class2">Bob</a>
   
   <a routerLink="/user/bob" [routerLinkActive]="['class1', 'class2']">Bob</a>
   
   <a routerLink="/user/bob" routerLinkActive="active-link"[routerLinkActiveOptions]="{exact: true}">Bob</a> // 精确匹配
   
   <a routerLink="/user/bob" routerLinkActive #rla="routerLinkActive">
     Bob {{ rla.isActive ? '(already open)' : ''}}
   </a>
   // 子节点匹配，父节点添加css
   <div routerLinkActive="active-link">
     <a routerLink="/user/jim">Jim</a>
     <a routerLink="/user/bob">Bob</a>
   </div>
   ```

   

6. 路由模块

   ```
   // app-routing.module.ts
   import { NgModule }              from '@angular/core';
   import { RouterModule, Routes }  from '@angular/router';
   
   import { HeroListComponent }     from './hero-list/hero-list.component';
   import { PageNotFoundComponent } from './page-not-found/page-not-found.component';
   
   const appRoutes: Routes = [
     { path: 'heroes',        component: HeroListComponent },
     { path: '',   redirectTo: '/heroes', pathMatch: 'full' },
     { path: '**', component: PageNotFoundComponent }
   ];
   
   @NgModule({
     imports: [
       RouterModule.forRoot(
         appRoutes,
         { enableTracing: true } // <-- debugging purposes only
       )
     ],
     exports: [
       RouterModule
     ]
   })
   export class AppRoutingModule {}
   
   // app.module.ts
   import { NgModule }       from '@angular/core';
   import { BrowserModule }  from '@angular/platform-browser';
   
   import { AppComponent }     from './app.component';
   import { AppRoutingModule } from './app-routing.module';
   import { HeroesModule }     from './heroes/heroes.module';
   
   import { PageNotFoundComponent } from './page-not-found/page-not-found.component';
   
   @NgModule({
     imports: [
       BrowserModule,
       FormsModule,
       HeroesModule,
       AppRoutingModule // 导入模块顺序必须approuting在最后
     ],
     declarations: [
       AppComponent,
       PageNotFoundComponent
     ],
     bootstrap: [ AppComponent ]
   })
   export class AppModule { }
   
   //heroes-routing.module.ts
   import { NgModule }             from '@angular/core';
   import { RouterModule, Routes } from '@angular/router';
   
   import { HeroListComponent }    from './hero-list/hero-list.component';
   import { HeroDetailComponent }  from './hero-detail/hero-detail.component';
   
   const heroesRoutes: Routes = [
     { path: 'heroes',  component: HeroListComponent },
     { path: 'hero/:id', component: HeroDetailComponent }
   ];
   
   @NgModule({
     imports: [
       RouterModule.forChild(heroesRoutes)
     ],
     exports: [
       RouterModule
     ]
   })
   export class HeroesRoutingModule { }
   
   // heroes.module.ts
   import { NgModule }       from '@angular/core';
   import { CommonModule }   from '@angular/common';
   import { FormsModule }    from '@angular/forms';
   
   import { HeroListComponent }    from './hero-list/hero-list.component';
   import { HeroDetailComponent }  from './hero-detail/hero-detail.component';
   
   import { HeroesRoutingModule } from './heroes-routing.module';
   
   @NgModule({
     imports: [
       CommonModule,
       FormsModule,
       HeroesRoutingModule
     ],
     declarations: [
       HeroListComponent,
       HeroDetailComponent
     ]
   })
   export class HeroesModule {}
   ```

   

7. 路由守卫

   - 多种路由守卫

     - 用[`CanActivate`](https://angular.cn/api/router/CanActivate)来处理导航*到*某路由的情况。
     - 用[`CanActivateChild`](https://angular.cn/api/router/CanActivateChild)来处理导航*到*某子路由的情况。
     - 用[`CanDeactivate`](https://angular.cn/api/router/CanDeactivate)来处理从当前路由*离开*的情况.
     - 用[`Resolve`](https://angular.cn/api/router/Resolve)在路由激活*之前*获取路由数据。
     - 用[`CanLoad`](https://angular.cn/api/router/CanLoad)来处理*异步*导航到某特性模块的情况。

   - 守卫冒泡

   - 无组件守卫

     ```
     
     {
         path: 'heroes', 
         children: [{ // 无组件路由，
             path: 'user',
             component: User
         }，{ 
             path: 'user',
             component: User
         }]
     },	
     ```

   - 通过服务实现守卫接口，根据返回boolean值判断

8. 异步路由

   ```
   // 8之前版本
   {
     path: 'admin',
     loadChildren: './admin/admin.module#AdminModule',
   },
   
   //8版本，类似vue
   {
     path: 'admin',
     loadChildren: () => import('./admin/admin.module').then(mod => mod.AdminModule),
   },
   ```

   

