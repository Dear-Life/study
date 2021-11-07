### 简介

```text
分布式版本控制系统
```

### 作用

```text
代码备份 版本回退 协作开发 权限控制
```

### 安装

```text
https://git-scm.com/
```

### 配置

```sh
git config --global user.name 'stefzi'
git config --global user.email 'stefzi0723@gmail.com'
git config -l
```

### 操作

```sh
git init
git add -A
git commit -m init
```

### 分支

```sh
git branch dev
git branch
git checkout dev
git merge dev
git branch -d dev
git checkout -b fix
git checkout -b dev origin/dev
```

### GitHub

```sh
git remote add origin https://github.com/Dear-Life/aaa.git
git push -u origin master
git pull origin master
git clone https://github.com/Dear-Life/test.git
```
