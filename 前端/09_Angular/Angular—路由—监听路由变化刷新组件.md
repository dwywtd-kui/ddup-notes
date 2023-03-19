## 监听路由变化进行处理
```typescript
import { Router, NavigationStart, NavigationEnd  } from '@angular/router';
import { filter } from 'rxjs/operators';

export class ArticleComponent implement OnInit, OnDestroy {
  
   // 声明订阅对象
  subscription : Subscription;

    constructor(private router: Router) { }

    ngOnInit() {
      this.subscription = this.router.events
      .pipe(
        filter(event => event instanceof NavigationEnd)
      ).subscribe(event=>{
        // 执行业务操作
        console.log(event)
        this.buildContent();
      }) 
    }

    ngOnDestroy() {
        this.subscription.unsubscribe(); // 不要忘记处理手动订阅
    }
}
```
假如路由处于 'article/2'，业务逻辑需要在这里重新定位到 'article/3' 时，这下就不仅仅是url发生变化了，页面也会随之被更新。

[https://zhuanlan.zhihu.com/p/54554069](https://zhuanlan.zhihu.com/p/54554069)
[https://www.jianshu.com/p/0902206df368](https://www.jianshu.com/p/0902206df368)

## 路由复用移除


**场景：**
使用的是同一个组件，但是路由的参数不一样
**需求：**
参数不同的时候，组件重新获取数据
**举例:**
articles?category=1&type=0 切换路由至 articles?category=1&type=1，我们想要的是根据参数再次获取数据，实际情况不会重新获取

**解决方案：**
```typescript
import { ActivatedRoute, Router } from '@angular/router';

constructor(
    private articleService: ArticleService,
    private routeInfo: ActivatedRoute,
    private router: Router
  ) {
    // override the route reuse strategy 复用路由
    this.router.routeReuseStrategy.shouldReuseRoute = () => {
      return false;
    };

  }
```
