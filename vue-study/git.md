# git学习 
[学习参考网址](https://www.liaoxuefeng.com/wiki/896043488029600)
## 配置
```
$ git config --global user.name "xzy"
$ git config --global user.email 394337123@qq.com
```
## 指令
### 创建一个版本库
##### 1.创建目录
```
- mkdir learngit
- cd learngit
- pwd
  /learngit
```
##### 2.将该目录变成 git 可以管理的仓库
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```
##### 3.编写一个文件（文件需放在仓库里）及上传
```
$ git add readme.txt
$ git commit -m "wrote a readme file"
```
### 常用指令
ls -ah 可以查看一些隐藏的目录
cat readme.txt 查看文件的内容
git -status 可以随时掌握工作区的状态
git diff 如果git -status告诉你有文件被修改过，用git diff 可以查看修改的内容
git log 可以告诉我们修改的历史记录 （git log --pretty=oneline）
git reset --hard HEAD^ 版本回退到上一个版本
$ git reset --hard a22f1    a22f1是指定的版本号 
git reflog用来记录你的每一次命令：
### 其它
- 可视化工具查看Git历史