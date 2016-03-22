title: 正确配置geoserver标签(label)的姿势
date: 2016-03-22 15:32:12
category: gis
tags: 室内地图
---
label是地图上不可或缺的元素，geoserver的label是在geoserver的style文件中配置的，以下是我生产环境中的label配置：
```
<Rule>
 <TextSymbolizer>
   <!--  配置显示label文字的属性，我这里是label -->
   <Label>
     <ogc:PropertyName>label</ogc:PropertyName>
   </Label>
   <Font>  
    <CssParameter name="font-size">12.0</CssParameter>  
    <CssParameter name="font-style">normal</CssParameter>  
    <CssParameter name="font-weight">bold</CssParameter>  
   </Font>
   <Fill>
     <CssParameter name="fill">#990099</CssParameter>
   </Fill>
   <!-- 取消默认的label重复显示 -->
   <Geometry>
      <ogc:Function name="centroid">
         <ogc:PropertyName>the_geom</ogc:PropertyName>
      </ogc:Function>
   </Geometry>
   <!-- label旋转角度 -->
   <LabelPlacement>
     <PointPlacement>
       <Rotation>
       45
       </Rotation>
     </PointPlacement>
   </LabelPlacement>
 </TextSymbolizer>
</Rule>
```