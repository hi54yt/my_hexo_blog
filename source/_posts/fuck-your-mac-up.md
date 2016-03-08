title: 打造全栈工程师最顺手的开发环境
date: 2016-03-01 21:20:16
categories:
  - Mac
tags:
---
本文适用于MAC操作系统，程序员的电脑就像职业车手的座驾，应该把开发环境应该调教到最佳状态。以下基于我常用的技术栈react native、rails、git，整理出该环境下的“武功秘籍”：
# Rails
## 第一式
招式：gem install时默认跳过ri、rdoc安装
步骤：打开 ~/.gemrc，加入gem: --no-ri --no-rdoc
心得：gem install默认会安装doc文件，十分浪费时间，我们有限的生命已经被GFW浪费够多的，这些小地方必须有寸土不让的精神。

# NPM
## 第一式
招式：更换npm源
步骤：
三种办法任意一种都能解决问题，建议使用第三种，将配置写死，下次用的时候配置还在:
1.通过config命令
    npm config set registry https://registry.npm.taobao.org 
    npm info underscore （如果上面配置正确这个命令会有字符串response）
2.命令行指定
    npm --registry https://registry.npm.taobao.org info underscore 
3.编辑 ~/.npmrc 加入下面内容
    registry = https://registry.npm.taobao.org

# Git
## 第一式
招式：增加git alias
步骤：
```
git config --global alias.alias command
```
For example, I use git status a lot, so a shorter alias would be nice:
```
git config --global alias.s status
```
This will add the following to your ~/.gitconfig file:
```
[alias]
  s = status
```
Now if I type git s I get the same output as git status. Of course you can always open ~/.gitconfig in a text editor and add s = status manually under the [alias] section.

from:<http://oli.jp/2012/git-powerup/>
