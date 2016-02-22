title: 处理fetch error
date: 2015-11-05 17:06
categories:
  - ReactNative
tags:
---
在react native里如果用了fetch，需要处理error，否则遇到网络无法连接等问题时，ios程序会直接崩溃.解决办法是用catch error:
```js
      fetch(endpoint + '/sites/' + this.props.siteId + '/devices.json')
        .then((response) => response.json())
        .then((response) => {
          this.setState({devices: response})
        })
        .catch((error) => console.log(error))
        .done()
```
<https://facebook.github.io/react-native/docs/network.html#async>
