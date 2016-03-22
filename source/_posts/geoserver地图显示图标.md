title: geoserver地图显示图标
date: 2016-03-22 14:05:39
category: gis
tags: 室内地图
---
geoserver地图上显示图标是常见的功能，比如一张室内地图上需要显示卫生间、电梯等图标。
{% qnimg icon_on_map.png title:wms地图 alt:wms地图 'class:class1 class2' extend:?imageView2/2/w/600 %}
根据网上的资料整理出以下步骤：
1.上传需要显示的图标到geoserver的styles目录下，一般生产环境下是这个目录：
`/var/lib/tomcat7/webapps/geoserver/data/styles`
2.配置地图的sld样式文件：
```
<Rule>
  <Name></Name>
  <ogc:Filter>
    <ogc:PropertyIsEqualTo>
      <ogc:PropertyName>type</ogc:PropertyName>
      <ogc:Literal>toilet</ogc:Literal>
    </ogc:PropertyIsEqualTo>
  </ogc:Filter>

 <PointSymbolizer>
     <Graphic>
        <ExternalGraphic>
           <OnlineResource xlink:type="simple" xlink:href="http://wms.smart-museum.cn/geoserver/styles/wc.png" />
           <Format>image/png</Format>
        </ExternalGraphic>
        <Size>20</Size>
     </Graphic>
   <VendorOption name="labelObstacle">true</VendorOption>
 </PointSymbolizer>
</Rule>
```
因为我们上传图片到styles目录，所以xlink:href这个属性可以配置成绝对路径`xlink:type="simple" xlink:href="wc.png"`，但是我的服务器上不知道什么原因就是不行，所以这里配置了绝对路径。以后查明了原因在更新。