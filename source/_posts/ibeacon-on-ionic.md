title: 在ionic中使用ibeacon
date: 2016-04-28 10:20:13
category: ionic
tags:
  - 室内地图
  - ibeacon
---
在ionic中使用ibeacon，和native开发中的步骤几乎一致，只需以下几步：
```
//指定ibeacon的uuid和identifier，这些需要提前在ibeacon中配置好
var uuid = 'SD041XAE-152C-43F5-A7W8-4F7ED54E6DA9'
var identifier = 'myibeacon'

//创建locationManager代理
var delegate = new cordova.plugins.locationManager.Delegate()
cordova.plugins.locationManager.setDelegate(delegate);

//开始监听ibeacon事件
var beaconRegion = new cordova.plugins.locationManager.BeaconRegion(identifier, uuid)
cordova.plugins.locationManager.startMonitoringForRegion(beaconRegion)
  .fail(console.error)
  .done();
cordova.plugins.locationManager.startRangingBeaconsInRegion(beaconRegion)
  .fail(console.error)
  .done();

// required in iOS 8+
cordova.plugins.locationManager.requestAlwaysAuthorization()

//获取ibeacon监听事件
delegate.didRangeBeaconsInRegion = function(pluginResult) {
  console.log(pluginResult.beacons)
}
```
