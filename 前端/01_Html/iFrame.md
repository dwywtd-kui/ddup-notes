## 实现iFrame自适应高度
```html
<iframe id="iFrame1" name="iFrame1" width="100%" onload="this.height=iFrame1.document.body.scrollHeight" frameborder="0" src="index.htm"></iframe>
```
关键就在于 `onload="this.height=iFrame1.document.body.scrollHeight" `


