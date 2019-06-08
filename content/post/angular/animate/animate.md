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


3. 动画函数，简单使用

   ```
   // state()函数定义状态	
   state('open', style({
     height: '200px', // 样式属性使用小驼峰形式
     opacity: 1,
     backgroundColor: 'yellow'
   })),
   state('closed', style({
     height: '100px',
     opacity: 0.5,
     backgroundColor: 'green'
   }))
   
   // transition(转场状态方向，animate()函数)转场函数
   transition('open <=> closed', [
     animate('1s//持续时间 1s//延迟时间 ease-in//动画速度'，style)
   ]),
   
   // trigger()动画触发器
   @Component({
     selector: 'app-open-close',
     animations: [
       trigger('openClose', [
         state(...),
         ...
         transition(...),
         ...
       ]),
     ],
     templateUrl: `<div [@openClose]="toggle">...</div>;`,
     styleUrls: ['open-close.component.css']
   })
   export class OpenCloseComponent {
     isOpen = true;
   
     toggle() {
       this.isOpen = !this.isOpen;
     }
   
   }
   ```

4. 转场与触发器

   ```
   // 通配符状态可以在任意状态之间转换，备用值
   animations: [
     trigger('openClose', [
       state('open', style({
         height: '200px',
         opacity: 1,
         backgroundColor: 'yellow'
       })),
       transition('* => open', [
         animate('0.5s')
       ]),
     ]),
   ],
   
   //void状态为进入或离开页面的元素设置转场动画
   animations: [
     trigger('flyInOut', [
       state('in', style({ transform: 'translateX(0)' })),
       transition('void => *', [
         style({ transform: 'translateX(-100%)' }),
         animate(100)
       ]),
       transition('* => void', [
         animate(100, style({ transform: 'translateX(100%)' }))
       ])
     ])
   ]
   
   //:enter、:leave是void => * 和 * => void的别名
   transition ( ':enter', [ ... ] );
   transition ( ':leave', [ ... ] );
   trigger('myInsertRemoveTrigger', [
     transition(':enter', [
       style({ opacity: 0 }),
       animate('5s', style({ opacity: 1 })),
     ]),
     transition(':leave', [
       animate('5s', style({ opacity: 0 }))
     ])
   ])
   
   //:increment和:decrement
   trigger('filterAnimation', [
     transition(':enter, * => 0, * => -1', []),
     transition(':increment', [
       query(':enter', [
         style({ opacity: 0, width: '0px' }),
         stagger(50, [
           animate('300ms ease-out', style({ opacity: 1, width: '*' })),
         ]),
       ], { optional: true })
     ]),
     transition(':decrement', [
       query(':leave', [
         stagger(50, [
           animate('300ms ease-out', style({ opacity: 0, width: '0px' })),
         ]),
       ])
     ]),
   ])
   
   //[@.disabled]指令通过Boolean值禁用该指令所在元素及其子元素上的动画
   
   //trigger()函数回调
   <div [@openClose]="isOpen ? 'open' : 'closed'"
       (@openClose.start)="onAnimationEvent($event)"
       (@openClose.done)="onAnimationEvent($event)"
       class="open-close-container">
   </div>
   
   //关键帧动画keyframes()函数
   transition('* => active', [
     animate('2s', keyframes([
       style({ backgroundColor: 'blue', offset: 0 }),
       style({ backgroundColor: 'red', offset: 0 }),
       style({ backgroundColor: 'orange', offset: 0 })
   ]))
   
   //通配符*自动计算属性
   animations: [
     trigger('shrinkOut', [
       state('in', style({ height: '*' })),
       transition('* => void', [
         style({ height: '*' }),
         animate(250, style({ height: 0 }))
       ])
     ])
   ]
   ```

   

5. 复杂序列

   - `query()`用于查找一个或多个内部HTML元素
   - `stagger()`用于为多元素动画应用级联延迟
   - `group()`用于并行执行多个动画步骤
   - `sequence()`用于挨个顺序执行多个动画步骤

   ```
   // 多元素动画
   animations: [
       trigger('pageAnimations', [
         transition(':enter', [
           query('.hero, form', [
             style({opacity: 0, transform: 'translateY(-100px)'}),
             stagger(-30, [
               animate('500ms cubic-bezier(0.35, 0, 0.25, 1)', style({ opacity: 1, transform: 'none' }))
             ])
           ])
         ])
       ]),
     ]
   })
   export class HeroListPageComponent implements OnInit {
     @HostBinding('@pageAnimations')
   }
   
   // 并行动画
   animations: [
     trigger('flyInOut', [
       state('in', style({
         width: 120,
         transform: 'translateX(0)', opacity: 1
       })),
       transition('void => *', [
         style({ width: 10, transform: 'translateX(50px)', opacity: 0 }),
         group([
           animate('0.3s 0.1s ease', style({
             transform: 'translateX(0)',
             width: 120
           })),
           animate('0.3s ease', style({
             opacity: 1
           }))
         ])
       ]),
       transition('* => void', [
         group([
           animate('0.3s ease', style({
             transform: 'translateX(50px)',
             width: 10
           })),
           animate('0.3s 0.2s ease', style({
             opacity: 0
           }))
         ])
       ])
     ])
   ]
   
   // 顺序动画
   @Component({
     templete:`<ul class="heroes" [@filterAnimation]="heroTotal"></ul>`,
     animations: [
       trigger('filterAnimation', [
         transition(':enter, * => 0, * => -1', []),
         transition(':increment', [
           query(':enter', [
             style({ opacity: 0, width: '0px' }),
             stagger(50, [
               animate('300ms ease-out', style({ opacity: 1, width: '*' })),
             ]),
           ], { optional: true })
         ]),
         transition(':decrement', [
           query(':leave', [
             stagger(50, [
               animate('300ms ease-out', style({ opacity: 0, width: '0px' })),
             ]),
           ])
         ]),
       ]),
     ]
   })
   export class HeroListPageComponent implements OnInit {
     heroTotal = -1;
   }
   ```

   

6. 可复用动画

   ```
   AnimationOptions接口可以创建在不同组件之间服用的动画，使用animation()在独立的.ts文件中定义动画并导出，然后在组件代码中通过useAnimation()导入。
   import {
     animation, trigger, animateChild, group,
     transition, animate, style, query
   } from '@angular/animations';
   
   export const transAnimation = animation([
     style({
       height: '{{ height }}',
       opacity: '{{ opacity }}',
       backgroundColor: '{{ backgroundColor }}'
     }),
     animate('{{ time }}')
   ]);
   
   import { Component } from '@angular/core';
   import { useAnimation, transition, trigger, style, animate } from '@angular/animations';
   import { transAnimation } from './animations';
   
   @Component({
       trigger('openClose', [
         transition('open => closed', [
           useAnimation(transAnimation, {
             params: {
               height: 0,
               opacity: 1,
               backgroundColor: 'red',
               time: '1s'
             }
           })
         ])
       ])
     ],
   })
   ```

   

7. 路由转场动画

   ```
   //component.html
   <div [@routeAnimations]="prepareRoute(outlet)" >
     <router-outlet #outlet="outlet"></router-outlet>
   </div>
   
   //component.ts
   prepareRoute(outlet: RouterOutlet) {
     return outlet && outlet.activatedRouteData && outlet.activatedRouteData['animation'];
   }
   
   //animate.ts
   export const slideInAnimation =
     trigger('routeAnimations', [
       transition('HomePage <=> AboutPage', [
         style({ position: 'relative' }),
         query(':enter, :leave', [
           style({
             position: 'absolute',
             top: 0,
             left: 0,
             width: '100%'
           })
         ]),
         query(':enter', [
           style({ left: '-100%'})
         ]),
         query(':leave', animateChild()),
         group([
           query(':leave', [
             animate('300ms ease-out', style({ left: '100%'}))
           ]),
           query(':enter', [
             animate('300ms ease-out', style({ left: '0%'}))
           ])
         ]),
         query(':enter', animateChild()),
       ]),
       transition('* <=> FilterPage', [
         style({ position: 'relative' }),
         query(':enter, :leave', [
           style({
             position: 'absolute',
             top: 0,
             left: 0,
             width: '100%'
           })
         ]),
         query(':enter', [
           style({ left: '-100%'})
         ]),
         query(':leave', animateChild()),
         group([
           query(':leave', [
             animate('200ms ease-out', style({ left: '100%'}))
           ]),
           query(':enter', [
             animate('300ms ease-out', style({ left: '0%'}))
           ])
         ]),
         query(':enter', animateChild()),
       ])
     ]);
   ```

   