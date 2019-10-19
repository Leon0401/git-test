熟悉git操作的文档
--
--
操作目的： 删除远程仓库的.idea文件，但本地的文件保留。每次提交，不需要push此文件。
          要实现上面的目标很简单，只需几个命令就行。不过为了清楚命令的具体作用，还是从下面的几个概念了解开始。

git原理图中的专用名词含义为：

workspace：工作区，idea里写的代码，保存了就在workspace。
index/stage：暂存区，git add命令执行后，会将代码存入stage/index。
repository：仓库区（或本地仓库），git commit命令执行后，代码会存入repository中。
remote：远程仓库，git push之后，代码会存入remote。

1. .gitignore文件
    第一步，添加.gitignore文件，在里面添加内容：
                                          ./idea

    如果你工程代码中存在.gitignore文件，且含有上面的内容。但是却没有达到忽略效果的原因是：.gitignore文件只会ignore没有被staged的文件。也就是说，之所以.idea能push到remote远程仓库，是因为你已经执行了git add命令。

2. git中删除.idea
    第二步，执行命令git rm --cached -r .idea，该命令的作用是删除暂存区或分支上的文件，停止追踪指定文件，但该文件会保留在工作区。这样相当于stage中没有.idea文件。
    
3. 追踪.gitignore文件并提交
    第三步，执行命令git add .以及git commit -m "删除.idea"。
4. push变化内容到remote
    第四步，执行命令git push。
    
    