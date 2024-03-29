# 机器学习接口文档

## 一、接口描述

机器学习API主要用于根据给定的特征数据得到对应的预测结果。



## 二、数据要求

1. 单次请求最多不超过1000条数据，特征数据的每个值不超过512个字符。
2. 传入的特征数据列要与训练时的列保持一致，包括特征列数量和特征列字段类型。
3. 特征数据除了数字类型，其它均以字符串形式传输。如果特征数据的某一个值为空，用空字符串代替。



## 三、调用方法及URL

调用方法：post

请求URL：请先在机器学习中进行模型训练，模型发布成功后可以在模型详情中查看url



## 四、请求参数

1.header请求参数

   业务请求参数

| 字段名称     | 必须 | 类型   | 示例值                         | 说明     |
| ------------ | ---- | ------ | ------------------------------ | -------- |
| Content-Type | 是   | String | application/json;charset=UTF-8 | JSON格式 |

2.body请求参数

   业务请求参数

| 字段名称 | 必须 | 类型   | 示例值                   | 说明                           |
| -------- | ---- | ------ | ------------------------ | ------------------------------ |
| 无   | 是   | Object(Array) | [[1,2,"2019-08-21"],[3,7,"2019-08-22"]] | 需要预测的特征数据数组 |



## 五、请求代码示例

http post模型发布的url

```json
[
  [5,3,"Allen, Mr. William Henry","male",35,0,0,373450,8.05,"","S"],
  [6,3,"Moran, Mr. James","male","",0,0,330877,8.4583,"","Q"],
  [7,1,"McCarthy, Mr. Timothy J","male",54,0,0,17463,51.8625,"E46","S"],
  [8,3,"Palsson, Master. Gosta Leonard","male",2,3,1,349909,21.075,"","S"]
]
```



## 六、返回值说明

1. 返回参数

| 字段名称       | 类型          | 示例值        | 说明                                                         |
| -------------- | ------------- | ------------- | ------------------------------------------------------------ |
| code           | Number        | 10000         | 返回结果，10000表示成功，非10000为对应错误号；错误号对应错误详情请看下文 |
| message         | String        | 查询成功 | 参见下方错误码-系统级错误码                                                 |
| data    | Object        | {...}        | 查询结果                                               |

2. 业务返回参数

    data参数信息

| 字段名称       | 类型          | 示例值        | 说明                                                         |
| -------------- | ------------- | ------------- | ------------------------------------------------------------ |
| code           | Number        | 10000         | 返回结果，10000表示成功，非10000为对应错误码；参见下方错误码-业务级错误码 |
| predictResult  | Object(Array)        | [[...],[...]...]         | 预测结果数组                                     |
| +index        | Number        | 0         | 当前数据的行数，从0开始编号                                         |
| +code | Number | 100 | 该行数据对应的返回码，1000表示成功，非1000为对应错误码；参见下方错误码-业务级错误码-数据错误码                        |
| +message         | String        | success         | 该行数据返回码对应的信息，参加下方错误码-业务级错误码-数据错误码对应的错误信息                                                |
| +result    | String        | 0        | 该该行数据预测的结果值                                               |

   

## 七、返回示例

```json
{
    "code": 1000,
    "message": "request success",
    "data": {
        "code": 10000,
        "predictResult": [
            {
                "index": 0,
                "code": 1000,
                "message": "success",
                "result": 1
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
| -2             | 服务器内部错误      |
| 1010	        | 特征列数量有误           |
| 1011	        | 单个值超过512字符           |
| 1012	        | 字段类型不匹配           |
| 1100	        | 其他错误           |
| 2000             |  用户APPK错误      |
| 1100             |  API返回消息不是200      |
| 2100             | 网关内部异常      |


---

如果您对产品有使用或者其他方面任何问题，欢迎联系我们

---
