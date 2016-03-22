title: 打造顺手的开发环境
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

ref:<http://oli.jp/2012/git-powerup/>

# SSH
## 第一式
招式： 配置ssh config快速登录服务器
步骤：
打开~/.ssh/config，加入以下内容：
```
Host hubei
    HostName 192.168.40.11
    User hbsb
Host yzsjzx
    HostName 42.96.206.22
    User wwwuser
Host camus
    HostName 114.215.96.33
    User wwwuser
```
以后可以这样登录服务器：`ssh hubei`

# 其它
## 第一式
招式：禁用DS_Store 
步骤：
在命令行中执行：
        
        defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
删除系统中已经存在的DS_Store文件
        
        sudo find / -name ".DS_Store" -depth -exec rm {} \;
然后记得重启finder
        
        killall Finder
心得：
.DS_Store是Mac OS保存文件夹的自定义属性的隐藏文件，如文件的图标位置或背景色，相当于Windows的desktop.ini。这个文件经常会随着git提交到项目里，十分没必要。