这里是实验室对于 **Git** 考核的笔记  

# 提交并推送 hello.md 的完整流程
💡```     ```部分均在 **bash** 命令窗口进行
1. 克隆远程仓库（若尚未克隆）

```
git clone git@github.com:wm19940219/Tasks.git
cd Tasks
```

2. 创建 **hello.md** 文件

```
echo "# Hello 姚英" > hello.md
（将“姚英”替换为自己的姓名）
```

3. 添加文件到暂存区

```
git add hello.md
```

4. 提交到本地仓库

```
git commit -m "添加 hello.md"
```
若提示需要配置用户信息，先执行：

```
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

5. 推送到远程仓库

```
git push origin main
（若分支为 master 则改为 git push origin master）
```

6. 验证

刷新 **GitHub** 仓库页面，即可看到 **hello.md** 文件。


# 阶段二任务2

使用 **Git Bash** 在初次接触时确实有一定学习成本，需要***记住命令**、**处理错误**等（😭这点真的深有体会，错一点都不行，自己还不一定能发现错误❌️）  但对于熟悉命令行的人来说非常高效。

更方便、更高效的方式：

我目前知道且用过的： **GitHub Desktop** 内置的 **Git** 插件，通过按钮完成 **add、commit、push**。
