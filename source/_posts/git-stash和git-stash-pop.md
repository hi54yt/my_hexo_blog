title: git stash和git stash pop
date: 2015-11-02 10:03
categories:
  - git
tags:
---
在多人协作coding时，需要先commit在pull代码，这时可以用
   
    git stash

命令把不想commit的代码“储存”起来。等pull完成后，再使用

    git stash pop
    
还原，有冲突会提示。