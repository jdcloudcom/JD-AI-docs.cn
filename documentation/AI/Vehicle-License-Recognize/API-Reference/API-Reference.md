# 行驶证识别

## 一、接口描述 

### 1. 功能描述  

基于业界领先的深度学习技术，识别机动车行驶证正页的关键字段识别，包括号牌号码、车辆类型、所有人、住址、使用性质、品牌型号、车辆识别代号、发动机号码、注册日期、发证日期等关键字段，准确可靠！
  
### 2. 接口数据要求：  
> 1. 图片格式：jpg、jpeg、png、jfif、bmp
> 1. 图片大小：小于1M 

### 4. 接口使用：  

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/ocr_vehicle_recognition
```
### 2. 请求方式：  
https  `post`aiapi.jdcloud.com/jdai/ocr_vehicle_recognition
### 3. 请求参数    

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | String | 是 | image/jpg | 标准编码格式
Authorization | String | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
无 | binary | 是 | 无 | 图片内容，传入图片

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数  

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1001 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code|	int|	0|	参见[错误码](Error-Code.md)-业务级错误码
message|	string|	success|	状态码描述，参见[错误码](Error-Code.md)-业务级错误码
request_id|	string|	cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
resultData|	object|	{...}|	返回识别结果

resultData参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
owner | String | 鲍岩 | 所有人
number | String | 黑BG4363 | 号牌号码
character | String | 非营运 | 使用性质
address | String | 黑龙江省新河哈尔市建华区西大桥街道 | 住址
issue_date | String | 2014-04-24 | 发证日期
engine | String | DCN009090 | 发动机号码
model | String | 吉利美日牌MR7152L01 | 品牌型号
register_date | String | 2014-04-24 | 注册日期  
vin | String | L6T7824SXDN047867 |  车辆识别代码  
type | String | 小型轿车 | 车辆类型  

### 2、返回示例   


```
{
    "code": 0,
    "charge":false,
    "remain":0，
    "msg":"查询成功"，
    "result":{
        "resultData": {
            "owner": "鲍岩",
            "number": "黑BG4363",
            "character": "非营运",
            "address": "黑龙江省新河哈尔市建华区西大桥街道",
            "issue_date": "2014-04-24",
            "engine": "DCN009090",
            "model": "吉利美日牌MR7152L01",
            "register_date": "2014-04-24",
            "vin": "L6T7824SXDN047867",
            "type": "小型轿车"
        },
        "message": "success",
        "request_id": "7643fdec7e8e1ad80db55d57faa98150",
        "code": 0
    }
}

```

