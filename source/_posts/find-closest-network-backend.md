title: 实现最短路径查找服务端api
date: 2016-04-28 09:46:2
category: gis
tags: 室内地图
---
实现最短路径查找，需要服务端配合：
以ruby为例，首先创建一个私有方法，用来获取“附近”的node，作为开始位置和结束位置
```
def find_closest_network_node(x, y, floor)
  res = CONN.execute(%Q{SELECT verts.id as id FROM public.networklines_3857_vertices_pgr AS verts
                        INNER JOIN (select ST_PointFromText('POINT(#{x} #{y} #{floor})', 3857)as geom) AS pt
                        ON ST_DWithin(verts.the_geom, pt.geom, 100.0)
                        WHERE ST_Z(verts.the_geom) = #{floor}
                        ORDER BY ST_3DDistance(verts.the_geom, pt.geom) LIMIT 1})
  if res.ntuples != 0
    res.getvalue(0,0)
  else
    return false
  end
end
```

建立坐标系转换私有方法：
```
def unproject(lon, lat)
  src_prj = RGeo::CoordSys::Proj4.new("+proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +wktext  +no_defs")
  dest_prj = RGeo::CoordSys::Proj4.new("+proj=longlat +datum=WGS84 +no_defs")
  point = RGeo::CoordSys::Proj4::transform_coords(src_prj, dest_prj, lon, lat)
  {x: point[0], y: point[1]}
end
```

然后创建获取最短路径的geoJSON，以供前台展示用，比如leaflet等：

```
def map_path
  start_x = params[:start_x]
  start_y = params[:start_y]
  start_floor = Beacon.find_by_name(params[:start_minor].to_i).floor.num

  end_x = params[:end_x]
  end_y = params[:end_y]
  end_floor = Beacon.find_by_name(params[:end_minor].to_i).floor.num

  //获取开始位置和结束位置的node id
  start_node_id = find_closest_network_node(start_x, start_y, start_floor)
  end_node_id = find_closest_network_node(end_x, end_y, end_floor)

  //通过数据库查询最短路径的拓扑数据，指定返回的拓扑结果为geoJSON格式
  if start_node_id.present? && end_node_id.present?
    res = CONN.execute(%Q{SELECT seq, id1 AS node, id2 AS edge,
            total_cost AS cost, layer,
            type_id, ST_AsGeoJSON(wkb_geometry) AS geoj
            FROM pgr_dijkstra(
              'SELECT ogc_fid as id, source, target,
                   st_length(wkb_geometry) AS cost,
                   layer, type_id
               FROM public.networklines_3857',
              #{start_node_id}, #{end_node_id}, FALSE, FALSE
            ) AS dij_route
            JOIN  public.networklines_3857 AS input_network
            ON dij_route.id2 = input_network.ogc_fid})
  else
    return render nothing: true, status: 404
  end

  //拼装成leaflet所用的格式返回给客户端
  route_features = []

  res.each do |segment|

    seg_cost = segment['cost']      # cost value
    layer_level = segment['layer'].to_i   # floor number
    seg_type = segment['type_id']
    geojs = JSON.parse(segment['geoj'])         # geojson coordinates


    geojs["coordinates"].each do |geo|
      lon = geo[0]
      lat = geo[1]
      point = unproject(lon, lat)
      geo[0] = point[:x]
      geo[1] = point[:y]
    end

    # build geojson
    feature = { "type": "Feature",
                "geometry": geojs,
                "properties": {"floor": layer_level,
                               "length": seg_cost,
                               "type_id": seg_type}
              }
    route_features << feature
  end
  @path = { "type": "FeatureCollection",
    "features": route_features
  }

  respond_to do |format|
    format.json { render json: @path }
  end
end
```
