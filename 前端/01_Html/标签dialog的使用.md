
> 原文地址：https://wangdoc.com/html/elements.html

`<dialog>` 
----------------------------------

### 基本用法

`<dialog>`标签表示一个可以关闭的对话框。

```html
<dialog>
  Hello world
</dialog>
```

上面就是一个最简单的对话框。

默认情况下，对话框是隐藏的，不会在网页上显示。如果要让对话框显示，必须加上`open`属性。

```html
<dialog open>
  Hello world
</dialog>
```

上面代码会在网页显示一个方框，内容是`Hello world`。

`<dialog>`元素里面，可以放入其他 HTML 元素。

```html
<dialog open>
  <form method="dialog">
    <input type="text">
    <button type="submit" value="foo">提交</button>
  </form>
</dialog>
```

上面的对话框里面，有一个输入框和提交按钮。

注意，上例中`<form>`的`method`属性设为`dialog`，这时点击提交按钮，对话框就会消失。但是，表单不会提交到服务器，浏览器会将表单元素的`returnValue`属性设为 Submit 按钮的`value`属性（上例是`foo`）。

### JavaScript API 

`<dialog>`元素的 JavaScript API 提供`Dialog.showModal()`和`Dialog.close()`两个方法，用于打开 / 关闭对话框。

```javascript
const modal = document.querySelector('dialog');

modal.showModal();

modal.close();
```

开发者可以提供关闭按钮，让其调用`Dialog.close()`方法，关闭对话框。

`Dialog.close()`方法可以接受一个字符串作为参数，用于传递信息。`<dialog>`接口的`returnValue`属性可以读取这个字符串，否则`returnValue`属性等于提交按钮的`value`属性。

```javascript
modal.close('Accepted');
modal.returnValue 
```

`Dialog.showModal()`方法唤起对话框时，会有一个透明层，阻止用户与对话框外部的内容互动。CSS 提供了一个 Dialog 元素的`::backdrop`伪类，用于选中这个透明层，因此可以编写样式让透明层变得可见。

```css
dialog {
  padding: 0;
  border: 0;
  border-radius: 0.6rem;
  box-shadow: 0 0 1em black;
}

dialog::backdrop {
  
  background-color: rgba(0, 0, 0, 0.4);
}
```

上面代码不仅为`<dialog>`指定了样式，还将对话框的透明层变成了灰色透明。

`<dialog>`元素还有一个`Dialog.show()`方法，也能唤起对话框，但是没有透明层，用户可以与对话框外部的内容互动。

### 事件 

`<dialog>`元素有两个事件，可以监听。

*   `close`：对话框关闭时触发
*   `cancel`：用户按下`esc`键关闭对话框时触发

如果希望用户点击透明层，就关闭对话框，可以用下面的代码。

```javascript
modal.addEventListener('click', (event) => {
  if (event.target === modal) {
    modal.close('cancelled');
  }
});
```