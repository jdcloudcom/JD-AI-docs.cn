# 目标检测接口文档

## 一、接口描述

目标检测API主要用于识别传入图片中的多个目标，提供目标物体的所在位置、对应名称等要素。



## 二、接口数据要求

1. 图片格式：JPG、JPEG、PNG。
2. 图片像素尺寸：最小 30x30 像素，最大 4096x4096 像素。
3. 图片文件大小：4MB。
4. 图片长宽比：3：1以内。



## 三、调用方法及URL

调用方法：post

请求URL： 请先创建拖拽式或者自动化项目的目标检测进行模型训练，模型发布成功后可以在模型详情中查看url。



## 四、请求参数

1. header请求参数

   业务请求参数

| 字段名称     | 必须 | 类型   | 示例值                         | 说明     |
| ------------ | ---- | ------ | ------------------------------ | -------- |
| Content-Type | 是   | String | application/json;charset=UTF-8 | JSON格式 |

2. body请求参数

   业务请求参数

| 字段名称 | 必须 | 类型   | 示例值                   | 说明                           |
| -------- | ---- | ------ | ------------------------ | ------------------------------ |
| base64   | 是   | String | {"base64":"/9j/4AAQ..."} | 图片base64编码值，需去掉图片头 |



## 五、请求代码示例

http post模型发布的url

```json
{
	"base64" : "/9j/4AAQSkZJRgABAQAASABIAAD/4QBYRXhpZgAAT……"
}
```



## 六、返回值说明

1. 返回参数

| 字段名称      | 类型          | 示例值        | 说明                                                         |
| ------------- | ------------- | ------------- | ------------------------------------------------------------ |
| code          | Number        | 10000         | 返回结果，10000表示成功，非10000为对应错误码；参见下方错误码 |
| predictResult | Object(Array) | [{…}{...}...] | 图片中识别出的目标物体列表                                   |
| +classes      | String        | 车灯          | 目标物体所属类别名称                                         |
| +score        | Number        | 0.8027        | 目标物体预测置信度                                           |
| +coordinates  | Object        | {...}         | 目标物体所在位置                                             |
| ++ymin        | Number        | 0             | 目标物体最上位置对应图片高度的百分比                         |
| ++xmin        | Number        | 0.1742        | 目标物体最左位置对应图片宽度的百分比                         |
| ++ymax        | Number        | 0.5831        | 目标物体最下位置对应图片高度的百分比                         |
| ++xmax        | Number        | 0.8633        | 目标物体最右位置对应图片宽度的百分比                         |



## 七、返回示例

```json
{
    "code":10000,
    "predictResult":[
        {
            "classes":"车灯",
            "score":0.8027,
            "coordinates":{
                "ymin":0,
                "xmin":0.1742,
                "ymax":0.5831,
                "xmax":0.8633
            }
        },
        {
            "classes":"车轮",
            "score":0.7442,
            "coordinates":{
                "ymin":0,
                "xmin":0.1955,
                "ymax":1,
                "xmax":0.7551
            }
        }
    ]
}
```



## 八、错误码信息

1. 错误码

| 错误码（code） | 错误信息（message） |
| -------------- | ------------------- |
| 10310          | 缺少必要参数        |
| 10311          | 参数有误            |
| 10440          | 图片类型错误        |
| 10441          | 图片大小超过限制    |
| 10442          | 图片像素超过限制    |
| 10443          | 图片比例超过限制    |
| -2             | 服务器内部错误      |
| 2000             |  用户APPK错误      |
| 1100             |  API返回消息不是200      |
| 2100             | 网关内部异常      |

---

如果您对产品有使用或者其他方面任何问题，欢迎联系我们

---
