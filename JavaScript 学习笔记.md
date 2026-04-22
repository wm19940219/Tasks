# JavaScript – 让网页“活”起来
这些笔记都是在使用过程中边学边做得到的


## ✅ 必记基础语法
```
javascript
// 1. 找到元素
const btn = document.getElementById('copyEmailBtn');

// 2. 监听事件
btn.addEventListener('click', function() {
    // 这里写点击后要做的事
});

// 3. 改变内容或样式
element.style.display = 'none';   // 隐藏
element.classList.add('show');    // 添加类
```

## 🧩 JS用来：


|功能	|核心代码	|解释|
|:---:|:---:|:---:|
|复制邮箱|	navigator.clipboard.writeText('邮箱')	|把文字放到剪贴板|
|问答折叠|answer.classList.toggle('show')	|切换显示/隐藏答案|
|点击QQ群显示二维码	|tempQrcode.style.display = 'block'	|弹出一个浮层|
|返回顶部	|window.scrollTo({ top: 0, behavior: 'smooth' })	|平滑滚动到最上面|
|自定义确认框	|先显示一个隐藏div，再根据按钮决定是否执行复制	|比 alert 好看一万倍|


## 📦 折叠问答的完整代码（必背）

```
javascript


document.querySelectorAll('.faq-question').forEach(btn => {
    btn.addEventListener('click', () => {
        const answer = btn.nextElementSibling;
        const icon = btn.querySelector('.icon');
        answer.classList.toggle('show');
        icon.textContent = answer.classList.contains('show') ? '−' : '+';
    });
});
```

这段代码的意思是：找到所有问题按钮，点击时，找到紧挨着的答案，给它加上/去掉 **show** 类（**CSS** 里 `.show` 控制显示），同时把图标从 + 改成 −。


## 🧪 复制邮箱带确认框

```
javascript


document.getElementById('emailCopyBtn').addEventListener('click', async () => {
    const result = await showConfirm('邮箱复制好啦！😄'); // 自定义弹窗
    if (result) {
        navigator.clipboard.writeText('newthread_geek@outlook.com');
    }
});
```



## 🔍 调试JS的救命稻草

`console.log`(变量)：在控制台输出，看代码有没有执行到这一行。

用 `F12 → Sources` 打断点，让代码一行一行跑，就像看慢动作回放。
