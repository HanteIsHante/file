
# Git

##### Git取消跟踪某个文件
```
$git rm --cached FILENAME

```
如果后面跟的是目录就加上个 -r 就ok, 此操作不会删除这个文件


## Git  子模块

> 更新Submodule有两种方式:

1. 在父项目的目录下直接运行

```
git submodule foreach git pull
```

2. 在Submodule的目录下面更新

```
>cd 子模块
git pull

```

## Git修改分支名称

1. 本地分支重命名
```
Git branch -m oldbranchname newbranchname
```
2.远程分支重命名

如果修改远程分支，只需要将本地分支重命名为新分支名称，然后删除远程分支，再把本地分支上传就可以了
