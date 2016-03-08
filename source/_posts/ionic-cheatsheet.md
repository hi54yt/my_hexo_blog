title: ionic-cheatsheet
date: 2016-03-07 10:33:20
categories:
  - ionic
tags:
---
在开发ionic过程中，会遇到各种报错，尤其是新添加了cordova的plugin后，很容易因为依赖问题build不通过，一般采取重装plugin和platform来解决：

```
sudo npm update -g cordova
sudo npm update -g ionic
rm -rf plugins/
rm -rf platforms/
ionic platform add ios
ionic run ios
```