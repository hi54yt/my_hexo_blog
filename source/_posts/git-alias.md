title: git alias
date: 2015-10-27 09:40
categories:
  - save time
tags: git
---
增加git alias
Here’s the pattern to make an alias using git config:

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