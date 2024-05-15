**目的**

做这个项目主要是为了在实战中应用一下学到的数据结构知识，实现了一个简化版的git，完成了 init  \  add  \  commit  \  log  \  status  \  find  \  branch  \  checkout  \  reset  \  merge  \  rm这些命令。

##基本原理

**核心数据结构**

1. blob：git通过一个blob类型的对象存储文件的内容，通过 sha1算法计算每个文件的40位hashcode作为文件ID。
   - 只有文件名相同、文件内容相同才是相同文件，比如有一个a.txt（对应 blob1），在修改之后a.txt就不再和blob1对应，而是更新为blob2。
   - 这些blob数据结构，都存储在git目录下的 objects文件夹下。
2. tree：存储了工作目录结构，内容包括每个目录下每个文件（文件夹）的权限、文件名、id
3. commit：一个commit对应一个版本信息，可以理解为一个快照。
   - 包括目录结构tree的哈希值
   - 上一个commit的哈希值
   - 这个提交的备注信息、提交时间、作者等等
   - 单链表的数据结构
4. HEAD：存储当前工作目录所在分支。
   - HEAD可以理解为一个指针，指向当前的分支。
   - 这个分支信息存储在git目录下的ref文件夹里。refs/heads/文件夹存储所有的分支信息
   - HEAD--> refs/heads/cur_branch->cur_commit->tree->all data blobs
   - 本质上就是一个根据有向无环图，数据由Key值进行索引。
5. refs/heads：用来存储各个分支最新的commit，也即链表的末端。



## 工作分区

1、工作目录：也就是我们看到的目录文件夹

2、暂存区：记录待提交的文件。

3、Git仓库：保留了所有历史版本信息的文件目录

**文件夹目录设计**

- objects：存储git对象，blob（文本信息）、tree（目录信息）、commit（版本信息）
- refs：分支信息
- HEAD：记录当前所在分支，或当前所在commit
- index：暂存区，记录
- logs：提交的历史记录，可查看每次提交的具体信息。

**涉及的数据结构和算法**

- 链表：每一个分支的commit就是一个链表
- 树：tree中记录的文件夹目录结构
- 哈希：用来存储文件内容的blobs，就是用哈希来创建索引，用sha1算法求得40位的哈希值，取前两位做目录。
- BFS/DFS：checkout使用

## 核心操作

1. add

2. commit
3. merge

## 参考

git官方文档：https://git-scm.com/docs

git原理介绍：https://zhuanlan.zhihu.com/p/96631135

git技巧：https://www.lzane.com/tech/git-tips/

git merge: https://www.lzane.com/tech/git-merge/

git可视化

- https://marklodato.github.io/visual-git-guide/index-zh-cn.html
- https://onlywei.github.io/explain-git-with-d3/#commit  **强推**

工具：Maps, hashing, file I/O, graphs 

https://zhuanlan.zhihu.com/p/496809425

