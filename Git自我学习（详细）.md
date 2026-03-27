这里则是我接触何学习使用Git的历程和遇到的问题，还是那句话，万一有人遇到和我同样问题的新朋友呢？
# 认识  

## 下载

我接触 **Git** 最初是为了将本地记事本写的 **Markdown** 文档进行渲染和编辑，而且将其打包到 **GitHub** 里，查询后就有提到 **Git** ，于是直接在浏览器进行了下载。  

## 配置

我感觉 **Git** 和 **codeblocks** 有点像，它安装以后并不呈现在电脑桌面可以看得到,而是需要用到**命令窗口**（当然不止这一种打开方式）  
刚开始还需要对它进行配置，用来标记提交者信息（⭐这是必须要完成的步骤，相当于软件的注册登录？）  
👉执行两条命令：（当然，内容要写你的信息）  
`git config --global user.name"你的用户名"`  
`git config --global user.email"你的绑定邮箱"`  
👉执行 `git config --list`  如果能看到刚才输入的用户名和邮箱，就说明配置成功了  
👉推荐设置初始默认分支为行业通用的 **main** ,执行：`git config --global init.defaultBranch main`  

# 使用

我只配置完，那个 **GitHub** 就被我登进去了，我就又学到了一种可以直接上传本地 **Markdown** 的方法，就还没使用 **Git**。（下次研究 **Git**）

👆2026/3/26记

👇2026/3/27记

# 使用 Git Bush

1.首先，我觉得要认识到一点：**Git**是一个**命令行工具**，就是一切都在**命令窗口**上完成  
2.要完成“使用 **Git Bash** 提交并推送名为 `hello.md` 的文档到远程仓库，内容为 `#Hello+你的姓名”` 这一项任务，对于刚接触 **Git** 的朋友来说，简单也简单，复杂也是真复杂。  
**下面是我使用过程遇到的问题和解决方法及一些思路总结**：  

## 从零开始：我的 Git 远程传送实战记录
这是一篇真实的 **Git** 学习记录，记录了我在第一次使用 **Git Bash** 将文件推送到 **GitHub** 时遇到的各种问题，以及最终如何一步步解决。希望能帮助到同样刚接触 **Git** 的新朋友。

### 一、最初的想法
我需要在 **GitHub** 上创建一个 `hello.md` 文件，内容为 `# Hello` 姓名，并把它推送到我的远程仓库 **Tasks**。

我首先尝试直接在 **Git Bash** 里执行：  

```bash

git add hello.md   

git commit -m "添加hello.md"  

git push origin main
```    

但结果全是：  

```text  

fatal: not a git repository (or any of the parent directories): .git
```  

原因：我并没有把远程仓库克隆到本地，当前目录不是 **Git** 仓库。必须先有本地仓库，才能进行 **Git** 操作。

### 二、克隆远程仓库

我打开 **GitHub** 上的仓库页面`（https://github.com/wm19940219/Tasks) `，复制了 **HTTPS** 克隆地址，然后执行：  

```bash

git clone https://github.com/wm19940219/Tasks.git
```

结果报错：

```text

fatal: unable to access 'https://github.com/wm19940219/Tasks.git/': Received fatal failure: Connection was reset
```  

原因：**HTTPS** 连接被网络环境阻断（可能是防火墙、代理或运营商限制）。

### 三、改用 **SSH** 方式

1. 生成 **SSH** 密钥  
```bash

ssh-keygen -t ed25519 -C "我的邮箱@example.com"
``` 

一路回车，密钥生成在 `~/.ssh/id_ed25519（私钥）和 ~/.ssh/id_ed25519.pub（公钥）`。

3. 查看公钥并添加到 **GitHub**  
```bash

cat ~/.ssh/id_ed25519.pub
```  

复制输出内容，在 **GitHub** 页面右上角头像 → **Settings** → 左侧找到 **SSH and GPG keys** → **New SSH key**，粘贴公钥，**Title** 任意。

5. 测试 **SSH** 连接

```bash

ssh -T git@github.com
```  

首次连接会提示确认指纹，输入 **yes**，然后看到：  


```text

Hi wm19940219! You've successfully authenticated, but GitHub does not provide shell access.
```  

说明 **SSH** 认证成功。

### 四、用 **SSH** 克隆仓库
我复制了 **SSH** 地址（仓库页面 `Code → SSH`），执行：  


```bash

git clone git@github.com:wm19940219/Tasks.git
```  

但注意，我一开始把仓库名写成了 `TasksPublic`，导致：  


```text

ERROR: Repository not found.
```  

纠正：确认仓库名是 **Tasks**，改为正确地址后克隆成功：  


```bash

git clone git@github.com:wm19940219/Tasks.git
```  

输出显示：  


```text

Cloning into 'Tasks'...

remote: Enumerating objects: 47, done.  

...

Resolving deltas: 100% (17/17), done.
```  

### 五、进入仓库并创建文件

```bash

cd Tasks
```

我尝试用 **echo** 创建 **hello.md**：  


```bash

echo "# hello 姚英 > hello.md"
```  

这里我把 **>**放在了引号内，导致 **echo** 只是输出了字符串，并没有创建文件。随后执行 `git add hello.md` 报错：  


```text

fatal: pathspec 'hello.md' did not match any files
```  

正确写法：**>** 放在引号外面。


```bash

echo "# hello 姚英" > hello.md
```  

检查文件内容：  


```bash

cat hello.md
```  

显示 `# hello 姚英`，正确。

### 六、添加、提交、推送
1. 添加文件
  
```bash

git add hello.md
```   

3. 提交  
```bash

git commit -m "添加 hello.md"
```  

这时报错：  


```text

Author identity unknown  

*** Please tell me who you are.
```  

原因：**Git** 需要知道提交者的姓名和邮箱。  


解决：设置全局用户信息（只需一次）：  


```bash

git config --global user.name "Yao Ying"  

git config --global user.email "wm19940219@example.com"  

（邮箱用 GitHub 注册邮箱）
```  

再次提交：  


```bash

git commit -m "添加 hello.md"
```  

成功。  

3. 推送到远程
先查看当前分支：
  

```bash

git branch
```  

显示 `* main`，说明分支是 `main`，执行：  


```bash

git push origin main
```  

输出显示推送成功。  

### 七、验证结果
刷新 **GitHub** 仓库页面 `https://github.com/wm19940219/Tasks`，果然看到了新上传的 `hello.md` 文件，内容为 `# hello 姚英`。

### 八、总结与心得
| 步骤	| 关键命令	| 可能遇到的问题|
|:------|:-------:|:-------------|
| 克隆仓库	| `git clone <地址>`	| HTTPS 连接失败 → 改用 SSH；地址写错 → 核对仓库名 |
| 生成 SSH 密钥	| `ssh-keygen -t ed25519`	| 无 |
| 添加公钥	| `GitHub Settings → SSH and GPG keys`	| 找不到入口 → 点击右上角头像选 Settings |
| 测试 SSH	| `ssh -T git@github.com`	| 首次需输入 `yes` |
| 进入仓库 |	`cd Tasks`	| 确保在克隆后的目录内 |
| 创建文件	| `echo "内容" > 文件名` | > 位置错误 → 放在引号外 |
|添加	| `git add <文件>` | 文件不存在 → 先确认文件已创建 |
| 提交 | `git commit -m "信息"` |	未配置用户信息 → `git config --global user.name/email` |
|推送 |	`git push origin main` |	分支名不匹配 → `git branch` 查看 |
整个过程中，我深刻体会到：

**耐心阅读错误信息**：大多数问题都能从提示中找到线索。  

**SSH 比 HTTPS 更稳定**：在国内网络环境下，**SSH** 往往能绕过一些限制。  

**Git 是命令行工具**：初学时容易在细节上出错（比如空格、引号），多练习就会熟练。  

希望我的这份记录能帮助新朋友们少踩一些坑，顺利开始 **Git** 之旅！


