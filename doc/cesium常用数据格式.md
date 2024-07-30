# cesium 中的数据格式

## geojson
常见的二维矢量数据格式（常规json的升级版），

```json
{
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "properties": {},
            "geometry": {
                "coordinates": [
                    [
                        [
                            116.28413009214364,
                            40.09126930439871
                        ],
                        [
                            116.12888873758385,
                            40.06670632732545
                        ],
                        [
                            116.10674395599347,
                            39.97034992991155
                        ],
                        [
                            116.16831311654528,
                            39.76814709175818
                        ],
                        [
                            116.42953771693556,
                            39.800336421693515
                        ],
                        [
                            116.59959392057402,
                            39.860897215717756
                        ],
                        [
                            116.72035753461711,
                            39.9289661601193
                        ],
                        [
                            116.79922046954391,
                            40.036603036700996
                        ],
                        [
                            116.72035661147544,
                            40.15913929437198
                        ],
                        [
                            116.49357330739451,
                            40.183566365375356
                        ],
                        [
                            116.28413009214364,
                            40.09126930439871
                        ]
                    ]
                ],
                "type": "Polygon"
            }
        },
        {
            "type": "Feature",
            "properties": {},
            "geometry": {
                "coordinates": [
                    [
                        [
                            116.87570049149116,
                            40.10005551184781
                        ],
                        [
                            116.87570049149116,
                            39.92941340167931
                        ],
                        [
                            117.11994082729757,
                            39.92941340167931
                        ],
                        [
                            117.11994082729757,
                            40.10005551184781
                        ],
                        [
                            116.87570049149116,
                            40.10005551184781
                        ]
                    ]
                ],
                "type": "Polygon"
            }
        }
    ]
}
```

## shapefile
esri公司创造的矢量数据格式，至少包含三个文件（.shp | .dbf | .shx），常见的二维矢量数据格式，在前端开发中通常将其读取并转为geojson处理。

## czml

1. 一个CZML文档包含一个JSON数组，数组中每一个对象都是一个CZML数据包（packet），一个packet对应一个场景中的对象，例如一个飞机。
2. 下面是CZMl一个包的全部详细属性

- id - 字符串:
    此数据包描述的对象的ID。ID不需要是GUID，但它们确实需要唯一地标识CZML源中的单个对象以及加载到同一范围内的任何其他CZML源。如果未指定此属性，客户端将自动生成唯一的属性。但是，这会阻止以后的数据包引用此对象以向其添加更多数据         
- delete - 布尔值:
    客户端是否应删除由ID标识的此对象的所有现有数据。如果为true，则将忽略此数据包中的所有其他属性
- name - 字符串:
    对象的名称。它不必是唯一的，旨在供用户使用
- parent - 字符串:
    父对象的ID（如果有）
- description - 字符串:
    对象的HTML描述
- clock - Clock:
    整个数据集的时钟设置。仅对文档对象有效
- version - 字符串:
    CZML 版本
- availability - TimeIntervalCollection:
    对象数据可用的时间间隔集。该属性可以是指定单个间隔的单个字符串，也可以是表示间隔的字符串数组。如果更改或发现不正确，以后的Cesium数据包可以更新此可用性
- properties - CustomProperties:
    此对象的一组自定义属性
- position - Position:
    物体在世界上的位置。该位置没有直接的可视化表示，但它用于定位附加到对象的广告牌，标签和其他图形项。
- orientation - Orientation : 
    世界上物体的方向。方向没有直接的可视化表示，但它用于定向模型，圆锥，金字塔和附加到对象的其他图形项
- viewFrom - ViewFrom:
    查看此对象时建议的相机位置。该属性被指定为相对于对象位置的East（x），North（y），Up（z）参考系中的笛卡尔位置
- billboard - Billboard:
    广告牌或视口对齐的图像，有时称为标记。广告牌由position属性定位在场景中
- box - Box:
    一个盒子，是一个封闭的长方体。使用position和orientation属性定位和定向框。
- corridor - Corridor:
    是由中心线和宽度定义的形状
- cylinder - Cylinder:
    由长度，顶部半径和底部半径定义的圆柱体，截锥体或圆锥体。使用position和orientation属性定位和定向圆柱体。
- ellipse - Ellipse:
    是地球表面上的闭合曲线。使用position属性定位椭圆。
- ellipsoid - Ellipsoid:
    是一个闭合的二次曲面，是椭圆的三维模拟。使用position和orientation属性定位和定向椭圆体。
- label - Label:
    一串文字。标签由position物业定位在场景中
- model - Model:
    3D模型。使用position和orientation属性定位和定向模型。
- path - Path:
    是由对象随时间的运动定义的折线。路径的可能顶点由position属性指定
- point - Point:
    点或视口对齐的圆。该点由position物业定位在场景中
- polygon - Polygon:
    是地球表面上的封闭图形
- polyline - Polyline:
    是由多个线段组成的场景中的线。
- rectangle - Rectangle:
    一个制图矩形,符合地球的曲率，可以沿表面或海拔高度放置
- wall - Wall:
    二维墙，符合地球的曲率，可以沿表面或高度放置
- agi_conicSensor - ConicSensor:
    考虑到椭圆体（即球体）的遮挡的锥形传感器体积。使用position和orientation属性定位和定向传感器。
- agi_customPatternSensor - CustomPatternSensor:
    考虑到椭圆体（即球体）的遮挡的自定义传感器体积。使用position和orientation属性定位和定向传感器
- agi_rectangularSensor - RectangularSensor:
    考虑椭圆体（即球体）遮挡的矩形金字塔传感器体积。使用position和orientation属性定位和定向传感器。
- agi_fan - Fan:
    它从一个点或顶点开始，并从顶点指定的方向列表中延伸
- agi_vector - Vector:
    定义源自position属性的图形矢量，并在提供的方向上延伸所提供的长度。使用position属性定位矢量。

