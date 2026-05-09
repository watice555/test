# git 个性化

## 设置git的用户名和邮箱

用户级别设置
```
git config --global user.name "watice"
git config --global user.email "w1825692103@gmail.com"
```
查询
```
git config --global --list
```


## 设置git代理

git config --global http.proxy http://127.0.0.1:7890
> 此为clash代理端口

# Git 通用基本用法

## 1. 初始化仓库

在项目目录里执行：

```bash
git init
```

作用：把当前目录变成一个 Git 仓库。

如果是从 GitHub 克隆已有项目：

```bash
git clone 仓库地址
```

例如：

```bash
git clone https://github.com/user/project.git
```

---

## 2. 查看当前状态

```bash
git status
```

这是最常用的命令之一，可以看到：

* 哪些文件被修改了
* 哪些文件还没有被 Git 跟踪
* 哪些文件已经加入暂存区
* 当前在哪个分支

---

## 3. 添加文件到暂存区

添加某个文件：

```bash
git add 文件名
```

添加所有变化：

```bash
git add .
```

注意：`git add` 只是把文件放进“准备提交”的区域，还没有真正保存成版本。

---

## 4. 提交版本

```bash
git commit -m "提交说明"
```

例如：

```bash
git commit -m "初始化项目"
```

提交说明建议写清楚这次改了什么，比如：

```bash
git commit -m "添加登录页面"
git commit -m "修复图片加载错误"
git commit -m "更新基金估值配置"
```

---

## 5. 重置提交 (git reset)

`git reset` 用于撤销提交或重置到某个提交状态。有三种主要模式：

### --soft 重置
```bash
git reset --soft <commit>
```
* 移动 HEAD 到指定提交
* 暂存区和工作目录保持不变
* 适合撤销提交但保留修改内容

例如，撤销最后一次提交但保留修改：
```bash
git reset --soft HEAD~1
```

### --mixed 重置 (默认)
```bash
git reset --mixed <commit>
# 或简写
git reset <commit>
```
* 移动 HEAD 到指定提交
* 更新暂存区以匹配指定提交
* 工作目录保持不变
* 适合撤销暂存但保留工作目录修改

撤销暂存某个文件：
```bash
git reset HEAD <文件名>
```

### --hard 重置
```bash
git reset --hard <commit>
```
* 移动 HEAD 到指定提交
* 更新暂存区和工作目录以匹配指定提交
* **警告：会丢失工作目录的未提交修改**

重置到上一个提交并丢弃所有修改：
```bash
git reset --hard HEAD~1
```

### 常用场景
* 撤销最后一次提交：`git reset --soft HEAD~1`
* 撤销暂存：`git reset HEAD <文件>`
* 完全重置到某个提交：`git reset --hard <commit-hash>`

## 5. 查看提交历史

```bash
git log
```

简洁版：

```bash
git log --oneline
```

效果类似：

```text
a1b2c3d 修复登录问题
e4f5g6h 添加首页
```

---

## 6. 查看文件改了什么

查看尚未提交的修改：

```bash
git diff
```

查看已经 `git add` 到暂存区的修改：

```bash
git diff --cached
```

---

## 7. 连接远程仓库

例如 GitHub 上创建了一个仓库后，可以连接：

```bash
git remote add origin 仓库地址
```

例如：

```bash
git remote add origin https://github.com/user/project.git
```

查看远程仓库：

```bash
git remote -v
```

---

## 8. 推送到 GitHub

第一次推送通常用：

```bash
git push -u origin main
```

之后可以直接：

```bash
git push
```

如果你的默认分支叫 `master`，则是：

```bash
git push -u origin master
```

---

## 9. 从远程拉取更新

```bash
git pull
```

它相当于从 GitHub 下载别人或其他设备上的新提交，并合并到本地。

---

## 10. 分支基本操作

查看分支：

```bash
git branch
```

创建新分支：

```bash
git branch 分支名
```

切换分支：

```bash
git switch 分支名
```

创建并切换：

```bash
git switch -c 分支名
```

例如：

```bash
git switch -c dev
```

合并分支：

```bash
git switch main
git merge dev
```

---

## 11. 撤销修改

### 撤销某个文件的未提交修改

```bash
git restore 文件名
```

例如：

```bash
git restore config.json
```

这会丢弃该文件的本地修改，要小心。

### 取消暂存

如果你已经执行了 `git add`，但还没 commit：

```bash
git restore --staged 文件名
```

例如：

```bash
git restore --staged config.json
```

### 修改最近一次提交说明

```bash
git commit --amend -m "新的提交说明"
```

---

## 12. .gitignore 基本用法

`.gitignore` 用来告诉 Git 哪些文件不要跟踪。

例如：

```gitignore
node_modules/
.env
*.log
dist/
__pycache__/
```

常见需要忽略的文件：

```gitignore
# Python
__pycache__/
*.pyc
.venv/

# Node.js
node_modules/
dist/

# 密钥和环境变量
.env
*.key

# 日志
*.log
```

注意：**已经被 Git 跟踪的文件，即使后来写进 `.gitignore`，也不会自动取消跟踪。**

如果某个文件已经被 Git 管理，想让它以后不再进入 Git：

```bash
git rm --cached 文件名
```

例如：

```bash
git rm --cached .env
```

然后提交：

```bash
git commit -m "停止跟踪环境变量文件"
```

---

## 13. 最常见工作流

日常改代码后：

```bash
git status
git add .
git commit -m "说明这次修改"
git push
```

从 GitHub 更新本地：

```bash
git pull
```

---

## 14. 一个完整例子

假设你新建了一个项目：

```bash
cd my-project
git init
git add .
git commit -m "初始化项目"
git branch -M main
git remote add origin https://github.com/你的用户名/my-project.git
git push -u origin main
```

之后每次修改：

```bash
git add .
git commit -m "更新功能"
git push
```

---

## 15. 新手最需要记住的几个命令

```bash
git status
git add .
git commit -m "说明"
git push
git pull
git log --oneline
```

如果只记一条排查命令，记这个：

```bash
git status
```

它通常会告诉你下一步该怎么做。

---

