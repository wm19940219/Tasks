# CSS – 让网页变好看的化妆术 


## ✅ 必记三大选择器
```
css
/* 标签选择器：改所有同标签 */
body { background: white; }

/* 类选择器：最常用，前面有个点 */
.card { border-radius: 32px; }

/* ID选择器：前面有个#，一个页面只能用一次 */
#copyEmailBtn { background: blue; }
```


## 🧩 常用样式及效果(记不住的有难了)——不过很多编辑器都会自动补充
|代码	|效果|
| :-----: | :------: |
|display: flex;	|让子元素排成一行（超级好用）|
|justify-content: space-between;	|两端对齐|
|align-items: center;	|垂直居中|
|position: fixed; top: 0;	|固定导航栏，不随滚动条移动|
|padding: 20px;	|内边距，让内容不贴边|
|margin-bottom: 40px;	|外边距，拉开距离|
|border-radius: 20px;	|圆角，变得可爱|
|box-shadow: 0 4px 12px rgba(0,0,0,0.1);	|阴影，立体感|
|transition: 0.3s;	|动画过渡，配合hover使用|
|:hover { transform: translateY(-5px); }	|鼠标悬浮时向上移动|


## 🎨 使用的一些好东西：
卡片左右交替：`.card:nth-child(even) { flex-direction: row-reverse; }` → 偶数卡片图片在右边。

固定导航栏不遮挡内容：`body { padding-top: 70px; }` → 给固定栏留出空间。

图片悬浮浮动：`.hero-logo:hover { transform: translateY(-25px); }` → 一碰就飘。

透明背景：`background: transparent;` → 让底层背景图透出来。


## 🧪 调试小技巧
在浏览器里按 `F12 → Elements`，可以实时修改 **CSS** 看效果，不用反复保存刷新。


类名拼写错、忘记写单位 `px`、漏掉分号，都是最常见的❌️。遇到样式不生效，先检查这三个。
