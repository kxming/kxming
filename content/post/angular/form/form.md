---
title: "Form使用"
date: 2019-06-08T22:02:09+08:00
categories:
- angular
- form
tags:
- angular
- form
keywords:
- angular
- form
#thumbnailImage: //example.com/image.jpg
---

本教程将讲解如何在angular8.x表单。Angular表单是一个可选的服务，在它自己的`@angular/forms`包中。

<!--more-->

<!--toc-->

1. 响应式表单

   - 导入包

     ```
     import { ReactiveFormsModule } from '@angular/forms';
     
     @NgModule({
       imports: [
         // other imports ...
         ReactiveFormsModule
       ],
     })
     export class AppModule { }
     ```

     

   - 使用

     ```
     // component.ts
     import { Component } from '@angular/core';
     import { FormGroup, FormControl, FormBuilder, Validators, FormArray  } from '@angular/forms';
     
     @Component({
         selector: 'app-name-editor',
         templateUrl: './name-editor.component.html',
         styleUrls: ['./name-editor.component.css']
     })
     export class NameEditorComponent {
       	updateName() {
       		this.name.setValue('Nancy');
       	}
       	
       	profileForm = new FormGroup({
         		firstName: new FormControl('',[Validators.required,Validators.minLength(4),]),
                 address: new FormGroup({
           			street: new FormControl(''),
           			city: new FormControl(''),
         		})
       	});
       	或者
       	profileForm = this.fb.group({
         		firstName: ['', Validators.required],
                 address: this.fb.group({
           			street: [''],
           			city: [''],
         		}),
               aliases: this.fb.array([
                 this.fb.control('')
               ])
       	});
       	onSubmit() {
       		console.warn(this.profileForm.value);// 提交表单
        	};
        	
        	updateProfile() {
           this.profileForm.patchValue({
             firstName: 'Nancy',
             address: {
               street: '123 Drew Street'
             }
           });
         };
         get aliases() {
           return this.profileForm.get('aliases') as FormArray;
         };
         addAlias() {
           this.aliases.push(this.fb.control(''));
         }
     }
     
     //component.html
     
     <form [formGroup]="profileForm" (ngSubmit)="onSubmit()">
       
       <label>
         First Name:
         <input type="text" formControlName="firstName">
       </label>
       
       <div formGroupName="address">
           <h3>Address</h3>
     
           <label>
             Street:
             <input type="text" formControlName="street">
           </label>
     
           <label>
             City:
             <input type="text" formControlName="city">
           </label>
         </div>
     	<button type="submit" [disabled]="!profileForm.valid">Submit</button>
     </form>
     <div formArrayName="aliases">
         <h3>Aliases</h3> <button (click)="addAlias()">Add Alias</button>
     
         <div *ngFor="let address of aliases.controls; let i=index">
             <!-- The repeated alias template -->
             <label>
             Alias:
             <input type="text" [formControlName]="i">
             </label>
         </div>
     </div>
     <p>
       <button (click)="updateProfile()">Update Profile</button>
     </p>
     ```

     

   - 

2. 模板驱动表单

   - 导入包

     ```
     import { NgModule }      from '@angular/core';
     import { BrowserModule } from '@angular/platform-browser';
     import { FormsModule }   from '@angular/forms';
     
     @NgModule({
       imports: [
         BrowserModule,
         FormsModule
       ],
       declarations: [],
       providers: [],
       bootstrap: [ AppComponent ]
     })
     export class AppModule { }
     ```

   - 使用

     ```
     <div>
         <h1>Hero Form</h1>
         <form #heroForm="ngForm" (ngSubmit)="onSubmit()">
             <label for="name">Name</label>
             <input type="text" [(ngModel)]="model.name" #name="ngModel" id="name" required>
           
             <label for="alterEgo">Alter Ego</label>
             <input type="text" [(ngModel)]="model.alterEgo" #alterEgo="ngModel" id="alterEgo">
     
           <button type="submit" [disabled]="!heroForm.form.valid">Submit</button>
     
         </form>
     </div>
     ```

     