这是实验室对于 **GitHub** 考核的记录
## 创建 Tasks 仓库

## 学习 GitHub 

### 1.创建 `.md` 文件

### 2.美化主页

参考案例：

[abhisheknaiidu 的主页][case1] [case1]: https://github.com/abhisheknaiidu

💡 结构清晰，用标题和分隔线分区；大量使用 Shields.io 徽章展示技术栈；嵌入 GitHub 统计卡片与访客计数器，简洁专业。

[anuraghazra 的主页][case2] [case2]: https://github.com/anuraghazra

💡 作为统计卡片作者，他通过 URL 参数自定义主题；加入动态贡献图，让主页随提交实时更新，并突出个人项目。


### 3.网页部署

#### 一、准备工作
1.安装 Git

2.将主网页文件命名为 **index.html**（全小写）

3.所有图片、**CSS、JS** 放在同一文件夹内

#### 二、本地 Git 操作（在项目文件夹内）

```
bash


git init                     # 初始化仓库
git add .                    # 添加所有文件
git commit -m "首次提交"      # 提交到本地
```


#### 三、连接远程仓库

```
bash


git remote add origin https://github.com/你的用户名/仓库名.git

(或 SSH：git remote add origin git@github.com:用户名/仓库名.git)

git branch -M main
git push -u origin main
```

#### 四、开启 GitHub Pages


1.仓库页面 → **Settings** → **Pages**

2.**Branch** 选择 `main`，文件夹选` / (root)` → **Save**

3.等待 1-2 分钟，访问：

```
text
https://你的用户名.github.io/仓库名/
```

#### 五、更新网页


修改文件后重复：
```
bash


git add .
git commit -m "更新说明"
git push
```


#### ⚠️ 常见坑

1.必须要有 `index.html`  在根目录

2.文件名不要有空格/中文，推荐 小写+下划线

3.图片路径写相对路径（如 `img/logo.png`）。

4.推送失败检查远程地址和权限（用 **SSH** 或 **token**）。

