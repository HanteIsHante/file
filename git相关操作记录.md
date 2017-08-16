
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

