# 定义和用法
<video> 标签定义视频，比如电影片段或其他视频流


<video> 标签是 HTML 5 的新标签。
## 常用属性
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1039463/1592554331969-92789a76-715b-42d2-a920-ce925c563f23.png#align=left&display=inline&height=357&name=image.png&originHeight=357&originWidth=827&size=42915&status=done&style=none&width=827)
# 常见问题
## 解决video标签设置autoplay在浏览器还不能自动播放问题

代码：
```html
<video id="video1" controls="controls" autoplay="autoplay" width="300" height="240" loop="loop" muted="true">
 <source src="/1.mp4" type="video/ogg" />
 <source src="/1.mp4" type="video/mp4" />
</video>
```



解决思路加上`muted="true"` 把声音禁止掉

**原因是因为谷歌等浏览器在2018.4开始改为自有在用户交互了才可以播放解决方式3中、视频声音是静音、手动设置、video.js**

原文链接：[https://blog.csdn.net/dengpengquan/article/details/102420583](https://blog.csdn.net/dengpengquan/article/details/102420583)
