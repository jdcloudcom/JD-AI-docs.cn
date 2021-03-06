# 文本分类接口文档

## 一、接口描述

文本分类API主要用于对输入的文本进行分类检测。



## 二、文本要求

文本长度小于等于512字符。



## 三、调用方法及URL

调用方法：post

请求URL： 请先创建拖拽式或者自动化项目的文本分类中进行模型训练，模型发布成功后可以在模型详情中查看url。



## 四、请求参数

1.query请求参数

   公共请求参数

| 字段名称     | 必须 | 类型   | 示例值                         | 说明     |
| ------------ | ---- | ------ | ------------------------------ | -------- |
| neu_app_key | 是   | String | 90j3l329knb39204e3948204958n49c | 您的appkey，可在NeuHub买家中心控制台获取 |

备注：
    neu_app_key对应AppKey申请地址：http://neuhub.jd.com/user/baseInfo
    
2.header请求参数

   业务请求参数

| 字段名称     | 必须 | 类型   | 示例值                         | 说明     |
| ------------ | ---- | ------ | ------------------------------ | -------- |
| Content-Type | 是   | String | application/json;charset=UTF-8 | JSON格式 |

3.body请求参数

   业务请求参数

| 字段名称 | 必须 | 类型   | 示例值              | 说明                 |
| -------- | ---- | ------ | ------------------- | -------------------- |
| text     | 是   | String | {"text":"水果坏了"} | 需要检测的文本字符串 |

   

## 五、请求代码示例

http post模型发布的url

```js
Content-Type:application/json;charset=UTF-8
{
    "text" : "水果坏了"
}
```



## 六、返回值说明

1. 返回参数

| 字段名称       | 类型          | 示例值        | 说明                                                         |
| -------------- | ------------- | ------------- | ------------------------------------------------------------ |
| code           | Number        | 10000         | 返回结果，10000表示成功，非10000为对应错误码；参见下方错误码-业务级错误码 |
| predictResult  | Object        | {...}         | 文本检测结果                                                 |
| +prediction    | String        | MySQL         | 文本检测的结果分类名                                         |
| +thresholdList | Object(Array) | [{…}{...}...] | 文本检测置信度数组                                           |
| ++name         | String        | MySQL         | 文本分类名称                                                 |
| ++threshold    | Number        | 0.9815        | 该分类的置信度                                               |



## 七、返回示例

```java
{
    "code":10000,
    "predictResult":{
        "prediction":"MySQL",
        "thresholdList":[
            {
                "name":"MySQL",
                "threshold":0.9815
            },
            {
                "name":"idea",
                "threshold":0.0125
            },
            {
                "name":"dog",
                "threshold":0.0019
            },
            {
                "name":"cat",
                "threshold":0.0042
            }
        ]
    }
}
```



## 八、错误码信息

1. 错误码

| 错误码（code） | 错误信息（message） |
| -------------- | ------------------- |
| 10310          | 缺少必要参数        |
| 10311          | 参数有误            |
| 10551          | 文本长度超过限制    |
| -2             | 服务器内部错误      |
| 2000             |  用户APPK错误      |
| 1100             |  API返回消息不是200      |
| 2100             | 网关内部异常      |
