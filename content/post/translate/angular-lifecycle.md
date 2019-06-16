---
title: "Angular生命周期完全指南"
date: 2019-06-16T22:01:09+08:00
categories:
- translate
tags:
- angular
- lifecycle
- translate
keywords:
- translate
#thumbnailImage: //example.com/image.jpg
---

原文链接： [www.cuelogic.com](https://www.cuelogic.com/blog/angular-lifecycle)

<!--more-->

 ![](https://p3.ssl.qhimg.com/t01a04e10fcd5ea4388.jpg) Angular是一个流行的、广泛使用的客户端平台框架，近年来赢得了数百万开发人员的青睐. 随着Angular的出现，web和移动应用的构建变得非常简单。每年都会有新版本出现，Angular的生命周期也在不断演变。

> Angular is a prevalent, broadly used client-side platform that has won millions of developer’s hearts in recent years. With the emergence of the Angular platform, application building has become extensively easy both for web and mobile. There are new versions emerging each year and Angular lifecycle keeps on evolving.

该框架是由谷歌于2009年推出. [Angular团队](https://angularjs.org/) 的第一个项目AngularJS非常受欢迎，依赖于HTML和JavaScript。然而，在后期的版本，你可能发现JavaScript已经被TypeScript和其他现代脚本语言所取代。

> The platform was introduced by Google back in 2009. AngularJS the first initiative by the [Angular team](https://angularjs.org/) was extensively popular and was dependent on HTML and JavaScript. However, in the later versions, you can find that JavaScript got replaced by TypeScript and other modern scripting languages.

Angular使开发人员更自由的开发运行在web端，移动端和桌面端的[应用程序](https://cuelogic.com/custom-software-development)。随着时间的推移，Angular经历了许多修改，并在AngularJS之后引入了许多版本，直到Angular7，而且还在不断更新。

> Angular has given the developers the freedom to [develop applications](https://cuelogic.com/custom-software-development) that can run on web, mobiles, and desktop. With time Angular has undergone many modifications and has introduced many versions after AngularJS to Angular7 and still counting.

# **什么是Angular生命周期?**

每个Angularjs版本在其生命周期中都会经历不同的阶段。组件在Angular中有决定性的作用。这里我将谈论angular组件生命周期 以及它们如何影响所有版本的生命周期，无论是第一个版本还是最后一个版本。为了开发过程的流畅性，Angular管理它的所有组件。 与任何自然生命周期一样，每个组件都有自己的生命周期事件，比如出生、生命事件和死亡。

> Each Angularjs version goes through various phases in its lifecycle. Components have a critical job in Angular; here I will talk about the component lifecycle of Angular and how they impact the lifecycle of all versions be it the first or the ultimate. For the smoothness in the development process, Angular manages all its components. Like any natural lifecycle, each component has its lifecycle events like – birth, life events, and death.

值得注意的是，Angular本身监控着[Angular组件和指令](https://angular.io/guide/attribute-directives)的所有生命周期， 您必须了解生命周期，并牢记其结果，才能使您的应用程序顺利进行。下面我将分享的信息适用与组件和指令。

> It is interesting to notice that Angular itself oversees all the lifecycle of [angular Components and Directives](https://angular.io/guide/attribute-directives), you have to understand the lifecycle with the result in mind to have the smooth progress of your application. The following information that I will share applies to both components and directives.

组件是任何Angular版本的主要构建块。因此，理解它们，理解组件生命周期的处理步骤，变得极为重要，只有这样，它才能在应用程序的开发中实现。

> Components are the primary building block for any Angular version. So it becomes utmost important to understand them to understand the processing steps of the lifecycle of components, then only it can be implemented in the development of an application.

在Angular中，你会注意到最令人兴奋的事情是，每个组件都有一个生命周期，生命周期的每个阶段都是从初始化到销毁。组件生命周期通常经历八个不同的阶段。

> The most exciting thing that you will notice in Angular is each, and every component in it has a lifecycle, and every stage of a lifecycle goes from initialization to destruction. A component lifecycle goes typically through eight different stages.

当Angular组件被初始化的时候，它创建并显示其根组件。 然后设计并产生了它的子组件。对于在应用程序开发过程中加载的所有组件，它会一直检查数据绑定属性何时更改和更新。当组件不再使用时，它将接近死亡阶段，然后被抽取并从DOM中删除。有时，在发生这些事件时，您可能需要编写一些额外的代码。我试图最自然的展示组件的生命周期，现在让我们详细说明。

> When an Angular component gets initialized, it creates and presents its root components. Which then designed and produced its heirs. For all of the components that gets loaded during the development of the application, it keeps checking when the data binding properties are getting changed and updated. When the component is not utilized anymore, it approaches the death phase which is then decimated and is expelled from the DOM. Sometimes you may have to write some additional codes as these events take place. I have tried to present the most natural glimpse of lifecycle of component, now let us elaborate it.

## **生命周期钩子概览**

> **Lifecycle hook overview**

组件生命周期中的事件也称为“生命周期钩子”。您可能对术语生命周期钩子感到不舒服，但它只是开发人员可以在Angular应用程序中组件生命周期的特定时刻调用的简单函数。我们还可以说这些生命周期钩子是Angular在组件生命周期中发生肯定事件时引发的回调方法。在组件或指令的生命周期中有8种不同的钩子。

> The events in the life of a component are also referred to as “lifecycle hooks.” You may get uncomfortable with the term lifecycle hooks, but it is nothing but simple functions that a developer can call during a specific point of the life of a component in their Angular application. We can also state that these lifecycle hooks are callback method that Angular raises when a positive event happens in the lifecycle of a component. There are 8 distinct kinds of hooks in the lifecycle of a component or directive.

你可以从Angular核心库中导入钩子函数，将一些独特的组件合并到应用程序的生命周期中。开发人员可以通过实现Angular核心库中的一个或多个钩子接口来抓住生命周期中的关键时刻。钩子事件可以包含在应用程序的任何阶段，以获得对组件更好的控制。

> You can execute hooks from the Angular core library as well to consolidate some unique components into the lifecycle of your application. Developers can knock on to the significant moments of a lifecycle by actualizing one or more hook interfaces from the Angular core library. Hook events can be included at any stages of an application to get excellent control over the components.

例如：引入由Angular调用ngOnInit钩子函数的一个组件。

> For example: To introduce a component ngOnInit is summoned by Angular.

- 在组件输入属性改变的时候，Angular将调用ngOnChange。

- > For the changed input property of a component, ngOnChange is invoked by the Angular.

- 在组件销毁的时候，Angular将调用ngOnDestroy。

- > On the destruction of a component, ngOnDestroy is invoked by the Angular.

组件是TypeScript类，这就是为什么必须将每个组件都视为构造方法的主要原因。在生命周期钩子事件中，首先执行组件类的构造函数。要将依赖项注入组件，必须使用构造函数。 Angular首先执行构造函数，然后显式执行所有其他生命周期钩子方法。

> The components are TypeScript Class; this is the primary motivation why you have to consider every component as constructor method. In the lifecycle hook event, the constructor of the component class gets first executed. For injecting dependency into the component, you must make use of the constructor. Angular executes the constructor first then only execution of all other lifecycle hook methods occurs explicitly.

## **Constructor VS OnInit**

作为一名开发人员，您必须生成并引入组件。为此，您必须选择两个选项，要么使用构造函数，要么使用OnInit生命周期方法。随着组件的初始化，OnInit生命周期方法将被触发。

> Being a developer, it will be essential for you to generate your component and introduce it. For that you must settle on two options that are either you can utilize constructor or use OnInit lifecycle method. With the initialization of component, the OnInit lifecycle method gets triggered.

使用哪种方法是由自己的决定，但是许多人认为他们更喜欢使用ngOnInit进行声明或初始化，并且尽量不使用构造函数。

> Which method you like to use is your decision, but many people have opined that they prefer to use ngOnInit for declaration or initialization and try not to use the constructors.

### **接口**

> ### Interfaces

接口是连接到生命周期方法的基本工具，因为应用程序的组件类需要实现基本接口。至于视图的引入，应该触发实现接口的方法是“AfterViewInit”，用于实现该接口的方法是“ngAfterViewInit”。

> The interface is a fundamental instrument to hook into the lifecycle method, as the component class of your application needs to implement the essential interface. As for the introduction of view, the method that should be triggered to implement the interface is “AfterViewInit,” and the method for this is ” ngAfterViewInit.”

### **ngOnchanges**

当组件的数据绑定属性发生变化时，或者简单地说，当组件内的输入控件得到更新时，就会执行这个回调函数。Angular接收一个更改后的数据映射，该数据映射包含数据绑定属性的当前和以前的位置，并封装在一个简单的更改中。

> This callback function is sought after when the data-bound property variations happen for a component or in simple words, we can say this event gets executed as and when the input control gets renewed inside the component. A changed data map is received by the Angular containing the present and previous position of the data-bound property encased in a simple change.

如果子组件使用了公开的属性装饰器@Input，则使用这个生命周期钩子，父组件可以轻松地与其子组件通信。即使父元素偏离了输入属性，这个钩子也会在子组件中被调用。开发人员使用这个钩子来发现有关已更改的输入属性的详细信息，以及它是如何更改的。

> Using this lifecycle hook a Parent component can easily communicate with its child component if the property decorator exposes @InputDecorator of the child component. Even if the parent deviations the input property this hook gets summoned in the child component. Developers use this hook to discover the details about the input property that has been changed and how it got changed.

**属性：**

> **Properties:**

- 实际上，它可用于所有具有输入的组件。

- > It can be utilized practically in all the components that have input.

- 每当输入值更改时调用。

- > Gets invoked whenever the input value gets changed.

- 它在ngOnInit之前调用。

- > It gets the initial call to get raised before ngOnInit.

### **ngOnInit**

当Angular完成组件的创建和引入时，这个回调函数也会被初始化为Angular显示数据绑定属性。此事件仅在ngOnChanges事件之后和构造函数之后获得其调用。使用这个钩子，您可以初始化组件的逻辑。如前所述，这个钩子在ngOnChanges之后获得初始化，这意味着ngOnInit的所有属性都可以使用它的所有属性。在此钩子被触发之前，不能使用子指令的任何属性。

> When Angular has completed the creation and introduction of components this callback is invoked, it also gets initialized as Angular displays data-bound properties. This event gets its call only after ngOnChanges event and after the constructor. With this hook, you can initialize logic to your component. As it is already said, this hook gets initialization after ngOnChanges that means all the properties ngOnInit can use all its properties. Any of the child directive properties cannot be used before this hack gets triggered.

**属性：**

> **Properties:**

- 这个钩子初始化组件数据。

- > This hook initializes data for a component.

- 在设置输入值之后，这个钩子被调用。

- > After setting the input values, this hook gets its call.

- 默认情况下，Angular CLI会将这个钩子添加到所有组件中。

- > This hook is added by default by Angular CLI to all the components.

- 它仅调用一次。

- > It is called only for once.

### **ngDoCheck**

每当Angular 自身无法捕获组件或指令的变更输入属性时，就需要使用这个钩子函数。你甚至可以使用这个回调来进行逻辑检查。简而言之，通过这个钩子，您可以实现在组件中的自定义检查逻辑。

> This is most sought after hook whenever there is a vitality to review the input property of a component or directive. You can even use this call back for your logic check. In short, through this hook, you can do custom check for your logic that you want to implement in the component.

这个钩子在ngOnInit之后立即随需应变，即使组件的属性没有变化，这个钩子也有它的执行职责。如果Angular错误地检测输入属性中的任何变化，就会出现这个钩子来拯救它。

> This hook comes on demand instantly after ngOnInit, and this hook has its duty of execution even if there is no change in the property of a component. This hook arises to rescue if Angular miscarries to detect any change in the input property.

**属性：**

> **Properties:**

- 由Angular运行以检测任何更改。

- > Run by Angular to detect any changes.

- 用来进行变化检测。

- > Called for change detection.

### ngAfterContentInit

当第一次引入和检查组件的每个内容时，ngAfterContentInit将在ngDoCheck之后调用。只要Angular在组件视图中做了任何内容投影，就会实现这个方法。当属性被明确划分为ContentChild和ContentChildren并被完全初始化时，也会调用此方法。

> ngAfterContentInit becomes a demand next to ngDoCheck when every content of the components gets introduced and checked for the first time. This method is implemented as soon as Angular makes any content projection within a component view. This method is also called when the properties get clearly demarcated as ContentChild and ContentChildren and are fully initialized.

Angular可以在标签中使用这种方法包含外部子组件。在组件的整个生命周期中，这个钩子只获得一次调用。

> External child components can be included by Angular using this method within the tag. In the total lifecycle of a component, this hook gets call only for once.

**属性：**

> **Properties:**

- 在最初调用ngDoCheck之后。

- > After ngDoCheck it is called initially.

- 它被用来初始化内容。

- > It does its work by initializing the content.

### ngAfterContentChecked

这个钩子方法通过使用Angular变化检测机制来检查组件内容的修改，即使没有任何修改，它仍然会被执行。它在ngAftercontentInit之后获得调用，并且在每次执行ngDoCheck之后执行。它在子组件的初始化过程中扮演着重要的角色。

> This hook method accomplishes its work by investigating the modification in the content of the component using Angular change detection apparatus, and it still performs its task even if there is not at all any modification. It gets its call after ngAftercontentInit and also gets executed after every execution od ngDoCheck. It plays a big role in the initialization of the child component.

**属性：**

> **Properties:**

- 这个方法等待ngContentInit完成后才开始执行。

- > This method waits for ngContentInit to finish its execution to get started.

- 在所有ngDocheck之后执行。

- > Executed after all ngDocheck.

### ngAfterViewInit

这个生命周期方法在ngAfterContentChecked之后调用，并仅在组件上查找它。这与ngAfterContentInit非常相似，它只在所有组件视图及其子视图之后调用。

> This lifecycle method gets its call after ngAfterContentChecked and finds its use only on components. This is very much similar to ngAfterContentInit, and it gets invoked only after all the component view and its child view.

**属性：**

> **Properties:**

- 在视图初始化之后，它只调用一次。

- > After the initialization of view, it gets its call only for once.

### ngAfterViewChecked

这个Angular生命周期方法在检查组件视图和子视图时被触发。这个方法在ngAfterViewInit之后调用，并且为每个ngAfterContentChecked方法调用。和上面讨论的许多其他生命周期钩子一样，它也只适用于组件。

> This Angular lifecycle method gets triggered subsequently as it checks component’s view and child view. This method gets its call after ngAfterViewInit and then for every ngAfterContentChecked method. Like many other lifecycle hooks discussed above it is also applicable for components only.

当等待子组件的某些东西时，这个组件可能会有帮助。

> When something is awaited from the child component, this component can be helpful.

**属性：**

> **Properties:**

- 检查和初始化完成后，将调用它。

- > After the checking and initialization are done, this gets its called.

- 在每个ngAfterContentChecked方法完成后，这个方法就开始执行。

- > After every ngAfterContentChecked method finishes its job, this method starts its work.

### ngOnDestroy

这个生命周期钩子在Angular销毁所有组件或指令之后调用。在这里使用清理逻辑，取消所有可观察对象的订阅，并分离事件处理程序，这样做可以防止内存泄漏。

> This lifecycle hook gets its call after Angular destroys all the components or directives. This is the place where you can use your clean up logic and unsubscribe from all observable and detach from event handlers, by doing so you can prevent memory leakage.

**属性：**

> **Properties:**

- 在从DOM中删除组件之前调用。

- > Gets its call just before components get removed from DOM.

## **如何使用Angular生命周期钩子?**

> ###### How can you make use of Angular lifecycle hooks?

你应该做的事情如下:

> The things that you should follow are as under:

- 首先，必须导入钩子接口。

- > First, you have to import the hook interface.

- 在钩子接口中，应该声明组件或指令。

- > In the hook interface, you ought to announce the component or directive.

- 接下来，您应该生成钩子方法。

- > Next, you ought to generate the hook method.

导入钩子接口是最佳策略。

> The best strategy to import hook interfaces

从核心模块导入钩子接口是必不可少的。不需要在名称前添加前缀。

> Here the importing hook interface from the core module is essential. Adding prefix before the name is not required.

```
export class SpyDirective implements OnInit, OnDestroy { ….}; @angular/core’;
```

这段代码取自 [https://angular.io/guide/lifecycle-hooks](https://angular.io/guide/lifecycle-hooks)

> *The code is taken from https://angular.io/guide/lifecycle-hooks*

组件实现生命周期钩子的声明：

> Statement of the component that actualizes lifecycle hooks :

在接下来的阶段中，您需要执行实现OnInit接口的组件。它的代码结构如下所示。

> In the subsequent stages, you need to characterize the App component that executes the OnInit interface. The code structure for that is given below.

```
//export class AppComponent { ,
```

语法取自 [c-sharpcorner.com](http://c-sharpcorner.com/)

> *syntax taken from c-sharpcorner.com*

## **创建钩子方法**

> ###### Generating the hook methods

必须记住的一件事是“钩子”和“钩子方法”有相似的名称。

> One thing that you should remember is the “hook” and “hook method” must have the similar name.

就在组件生成的时候，钩子以下面描述的关联方式实现

> Right at the point when the components are made the hooks are implemented in the associated way depicted under

![](https://p4.ssl.qhimg.com/t01e1b34385c09dccd0.jpg)

但是，当创建带有子组件的组件时，会执行一些扩展。

> However, the arrangement of execution gets some expansion in it when components with the child are created.

![](https://p3.ssl.qhimg.com/t015ce0a1fa0cfe4798.jpg)

对于子组件，我们需要运行

> Now for child component again we have to run

![Generating Hook Methods_1](https://p4.ssl.qhimg.com/t01e1b34385c09dccd0.jpg)

这里，在ViewInit之后加入父类。

> Here again, joins the parent After ViewInit.

## **结论**

> **Conclusion**

在上面的文章中，我讨论了生命周期钩子及其在组件或指令的生命周期中发生的顺序。应该记住的一件事是，这些生命周期钩子同时适用于组件和指令。

> In the above article, I have discussed the lifecycle hooks and their sequence in which they occur in the lifecycle of a component or a directive. One thing you should remember is these lifecycle hooks apply to both components and directives.

作为一名开发人员，您必须知道组件在Angular中有多么重要，因此了解这些生命周期钩子同样非常重要。阅读本文之后，您已经了解了钩子以及它们在[AngularJS开发](https://cuelogic.com/angularjs-development)的生命周期中扮演的角色。您应该谨慎使用这些钩子，因为您的项目可能不需要所有的钩子，所以选择您需要的钩子。

> Being a developer you must know how much importance the component holds in Angular, so knowing about these lifecycle hooks is equally very important. After reading this article, you have gained the knowledge about the hooks and what role they play in the lifecycle of an [AngularJS development](https://cuelogic.com/angularjs-development). You should be cautious of using these hooks as all the hooks may not be needed for your project, so choose those which are necessary for you.