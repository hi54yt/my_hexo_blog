title: React Native各种坑
date: 2015-10-15 11:20
categories:
  - ReactNative
tags: 坑
---
# ios
## 调试
* iOS下react native真机调试的坑：
编译的时候报这个错误：_RCTSetLogFunction
需要进build settings关闭Dead code stripping选项
参考：<https://github.com/facebook/react-native/issues/2685>

### navigitor
* navigitor隐藏返回按钮，一般用在登录后的页面

```js
    this.props.navigator.push({
      title: '站点',
      component: Sites,
      passProps: { userId: userId },
      leftButtonTitle: ' ',
    })
```

***

# android
## 调试
* 虚拟机不要用android自带的
用这个：<https://www.genymotion.com>，官方的虚拟机很慢，这个简直就是life saver。
* 找不到RCTRootView.h
一般是没有执行npm install,如果还不能解决,试试先清缓存

```
rm -rf node_modules
```
```
npm cache clear && npm install
```

*** 

# Others