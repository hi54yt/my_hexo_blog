title: ionic-cheatsheet
date: 2016-03-07 10:33:20
categories:
  - ionic
tags:
---
在开发ionic过程中，会遇到各种报错，尤其是新添加了cordova的plugin后，很容易因为依赖问题build不通过，一般采取**重装plugin和platform**来解决：

```
sudo npm update -g cordova
sudo npm update -g ionic
rm -rf plugins/
rm -rf platforms/
ionic platform add ios
ionic run ios
```

安装plugin的时候，如果不想cordova plugin add xxx，而是**一次安装所有的plugin**：

```
ionic state reset
```
ref: https://forum.ionicframework.com/t/how-to-install-all-my-codrova-plugins-listed-in-package-json/21328