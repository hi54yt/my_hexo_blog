title: navigatior传递
date: 2015-10-21 14:32
categories:
  - ReactNative
tags:
---
今早在写代码时报错：
```
message: Cannot read property 'push' of undefined
```
通过翻看react native文档，发现这么一段话：

>A navigator is an object of navigation functions that a view can call. It is passed as a prop to any component rendered by NavigatorIOS.        

原来iOS的navigator默认传递navigator对象到props参数里了。如果不是通过navigator渲染的页面，需要自己手动写
```js
navigator={this.props.navigator}
```
比如通过tab进入的页面很容易忘记传navigator：
```html
        <ScrollableTabView edgeHitWidth={deviceWidth / 2}>
          <Summary tabLabel="概况"  siteId={this.props.siteId} />
          <Zones tabLabel="区域" siteId={this.props.siteId} onZoneSelected={this._onZoneSelected} />
          <Search tabLabel="搜索" siteId={this.props.siteId} navigator={this.props.navigator} />
        </ScrollableTabView>
```

<http://facebook.github.io/react-native/docs/navigatorios.html#navigator>
