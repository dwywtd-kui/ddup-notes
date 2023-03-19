## Angular 中的dom操作（原生 js）
```typescript
ngAfterViewInit(){
    var boxDom:any=document.getElementById('box');
    boxDom.style.color='red';
}

```
## Angular 中的 dom 操作（ViewChild）
1、定义模板（使用模板引用）
```html
<div #myDiv>11111</div>
```
2、使用@ViewChild定义模板引用变量
```typescript
import { Component ,ViewChild,ElementRef} from '@angular/core';

....

@ViewChild('myDiv',{static:true}) eleRef: ElementRef;

ngAfterViewInit(){
    let attrEl = this.eleRef.nativeElement;
}
```
myDiv要与模板中的 #myDiv对应，名字不能出错，eleRef是变量名


## 父子组件中通过 ViewChild 调用子组件

1. 在父组件模板引用子组件并给子组件定义一个名称
```html
<app-footer #footerChild></app-footer>

```

2. 在组件中使用ViewChild
```typescript
import { Component, OnInit ,ViewChild} from '@angular/core';
...
// ViewChild 和刚才的子组件关联起来
@ViewChild('footerChild',{static:false}) footer;
```
> Angular8 需要添加 {static:boolean}属性，必填


3. 调用子组件实例
```typescript
run(){
    this.footer.footerRun();
}
```

实例：
```html
<app-header #header></app-header>

<div #myBox>
   我是一个dom节点
</div>

<button (click)="getChildRun()">获取子组件的方法</button>

```
```typescript
import { Component, OnInit,ViewChild} from '@angular/core';

@Component({
  selector: 'app-news',
  templateUrl: './news.component.html',
  styleUrls: ['./news.component.scss']
})
export class NewsComponent implements OnInit {
  //获取dom节点
  @ViewChild('myBox',{static:false}) myBox:any;
  //获取一个组件
  @ViewChild('header',{static:false}) header:any;
  constructor() { }

  ngOnInit() {
  }

  ngAfterViewInit(): void {    
    console.log(this.myBox.nativeElement);
    this.myBox.nativeElement.style.width='100px';
    this.myBox.nativeElement.style.height='100px';
    this.myBox.nativeElement.style.background='red';
    console.log(this.myBox.nativeElement.innerHTML);
  }

  getChildRun(){
    //调用子组件里面的方法
     this.header.run();
  }
}

```

### 引入多个相同组件
```typescript
@ViewChildren(UeditorComponent)
myEditorList: QueryList<UeditorComponent>;
```

`@ViewChild` 的作用实际上就是父Component把子Component的东西拿过来用而已。

1. 整个Component拿（通过class名称)
```typescript
@ViewChild(TodoComponent) 
private todoList: TodoComponent
```

2. 拿html dom

直接获取子组件HTML页面中的DOM，该DOM需要用#命名。如:
```html
<div #domLabel>cba</div>
```
这个设置的命名，有个单独的名称，模板应用变量。

3. 


