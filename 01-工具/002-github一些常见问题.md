# 本地删除git远程仓库里的文件

进入到当前文件夹，使用 git bash：

```bash
# 将远程代码 pull 到本地
$ git pull
Already up-to-date

# 删除
$ git rm -rf README.md

# 删除之后，本地文件夹就不存在了，为了同步，再次提交
$ git commit -m "xxx"
$ git push -u origin master
```

# git移除远程仓库某个文件夹

有的时候，我可能本地直接修改了文件夹名或者文件名（没有使用 git bash 修改），当我提交时，会发现仓库竟然多了重复的内容，只是命名不同而已，很烦躁！

那么我们可以使用下面的命令解决这个烦躁的问题！

```bash
# -n 展示要删除的文件列表项预览 
# 要删除的文件名是 07-CSS
$ git rm -rn --cached "07-CSS/"

# 最终执行命令
$ git rm -r --cached "07-CSS/"

# 提交
$ git commit -m "xxx"
$ git push -u origin master
```