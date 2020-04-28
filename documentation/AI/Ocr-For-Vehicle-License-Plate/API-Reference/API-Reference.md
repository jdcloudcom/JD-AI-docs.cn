# 车牌识别

## 一、接口描述

### 1. 功能描述
> 基于业界领先的深度学习技术，利用光学字符识别技术，可对输入的图片自动识别车牌字段信息，识别准确率业内领先，稳定可靠

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 图片要求

> 1. 图片格式：jpg、jpeg、png、bmp
> 2. 图片大小：小于5M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/license_plate
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/license_plate

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/json | 标准编码格式

#### （2）query请求参数

#### （3）body请求参数（二选一）

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imageUrl | String | 是 | imageUrl=https://img10.360buyimg.com/n1/.....a43.jpg | 完整图片url
imageBase64Str | String | 是 | imageBase64Str=/9j/4AAQSk... | 图片base64编码

### 4. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


## 三、返回说明
### 1、返回参数

#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


#### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code|	int|	0|	参照四、错误码-业务错误码
message|	string|	success|	状态码描述
request_id|	string|	cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
resultData|	json|	{...}|	返回识别结果

resultData参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
probability | float | 0.9878 | 置信度
text | String | 京A12345 | 识别结果
location | array | [1086,570,1197,566,1197,601,1086,606] | 检测框坐标，依次是[x1,y1,x2,y2,x3,y3,x4,y4], 对应车牌的四个顶点的坐标，x1,y1 对应左上角，其他角点依顺时针方向编号。

### 2、返回示例

```JSON
{
    "code": 0,
    "resultData": [
        {
            "probability":0.9878,
            "text": "京A12345",
            "location": [1086,570,1197,566,1197,601,1086,606]
        },
        {
            "probability":0.976,
            "text":"京A98312",
            "location": [500,589,600,589,600,620,500,621]
        }
    ],
    "message": "success",
    "request_id": "815774d6ed6ca43e5d0cce316d36d822"
}
```

### 3、业务错误码
业务错误码（code）|对应message|说明
------|------|------
12001|"image does not exist"|图像不存在
12002|"image format error"|图像格式错误
12003|"image size error"|图像大小错误
12004|"parameter does not exit"|参数不存在
12005|"parameter value is null"|参数值为null
13002|"time out"|超时
13004|"no content recognition"|无内容识别
13005|"internel error"|内部错误