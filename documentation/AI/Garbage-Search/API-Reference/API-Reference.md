# 垃圾分类识别

## 图像识别
### 一、接口描述

#### 1. 功能描述
通过图片进行垃圾分类查询的能力

#### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

#### 3. 接口数据要求：
> 1. 图片格式：base64编码
> 2. 图片大小：小于2M
> 3. 图片base64不能为空
> 4. 图片像素尺寸：最小 30\*30 像素，最大 4096\*4096 像素
> 5. 图片长宽比：3：1以内

### 二、请求说明

#### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/garbageImageSearch
```

#### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/garbageImageSearch

#### 3. 请求参数

##### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imgBase64 | String | 是 | 图像Base64编码值，去掉图片头"data:image/png;base64,"| 查询内容，应为图像Base64编码值图片
cityId | String | 是 | 310000 | 国家标准城市编码，请求结果根据此参数指定城市的垃圾分类标准返回，当前支持城市：310000(上海市)、330200(宁波市)、610100(西安市)、440300(深圳市)、北京市(110000)

#### 4. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


### 三、返回说明
#### 1、返回参数

##### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


##### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status|	int|	0|	参照业务错误码
message|	string |	"success"|	参照业务错误码
garbage_info|	array |	[...]|	返回垃圾分类信息

garbage_info

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
garbage_name | string | 咖啡 | 垃圾名称
cate_name | string | 湿垃圾 | 垃圾分类
city_id | string | 310000 | 城市id
city_name | string | 上海市 | 城市名称
ps | string | 容器与外包装为可回收物 | 备注描述
confidence | float | 1 | 文本置信度恒为1

#### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": true,
  "remain": 4964,
  "remainTimes": 4964,
  "remainSeconds": -1,
  "msg": "查询成功,扣费",
  "result": {
    "status": 0,
    "message": "success",
    "garbage_info": [
      {
        "cate_name": "湿垃圾",
        "city_id": "310000",
        "city_name": "上海市",
        "confidence": 1.0,
        "garbage_name": "剩饭",
        "ps": "湿垃圾应从生产时就与其他品种垃圾分开收集。投放前尽量沥干水分，有外包装的应去除外包装投放"
      }
    ]
  }
}
```

#### 3、业务错误码
业务错误码（status）|对应message|说明
------|------|------
0|success|成功
4101|not enough param|缺少必要参数
4102|param error|参数有误
4103|Request Service Error!|图像请求过程失败
4104|Error image input|读取图像失败
4201|Image data is too large or too small|图片大小超过限制
4202|image type error|图片类型错误
4203|image pixel out of range|图片像素超过限制
4204|image proportion out of range|图片比例超过限制
4105|Unsupport search type|查询类型不支持
4106|imgBase64 is necessary|未提供查询内容
4107|City_id is invalid|无效的城市Id
4108|No match result|无匹配的搜索结果
5101|Internal Server Error|服务器内部错误

## 语音识别
### 一、接口描述

#### 1. 功能描述
提供通过语音进行垃圾分类查询的能力

#### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

#### 3. 接口数据要求：
>1. 目前⽀持的音频格式为:wav、mp3、amr
>2. 音频采样率为:16KHz
>3. 音频通道数:单通道
>4. 一次请求的音频最大时长:60秒

### 二、请求说明

#### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/garbageVoiceSearch
```

#### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/garbageVoiceSearch

#### 3. 请求参数

##### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）query请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
cityId | String | 是 | 310000 | 国家标准城市编码，请求结果根据此参数指定城市的垃圾分类标准返回，当前支持城市：310000(上海市)、330200(宁波市)、610100(西安市)、440300(深圳市)、北京市(110000)
property | jsonstring | 是 | {"autoend":false,<br>"encode":{<br>"channel":1,<br>"format":"wav",<br>"sample_rate":16000,<br>"post_process":0<br>},<br>"platform":"Linux",<br>"version":"0.0.0.1"} | 音频元数据

Property参数说明

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
autoend|bool|是|false|bool类型，是否开启服务端自动断尾检测功 能，默认填false;开启则填true
encode|object|是|{...}|语⾳识别的请求格式为:<br> \- channel:int类型，⾳频声道数，目前只⽀持单声道，填1<br> \- format:string类型，⾳频格式，支持wav， amr，mp3<br> \- sample_rate:int类型，采样率，目前只⽀持填写16000<br> \- post_process:int类型，数字后处理:1为强制开启(开启后，会把结果中的数字汉字转换成阿拉伯数字。例如，识别结果中的“一千”会 转成“1000”)，0为根据服务端配置是否进行数字后处理
platform |string |是 |iOS&iPhone X&11.4.1| 字符串串类型，各平台的机型信息<br> \- 格式:{平台}&{机型}&{系统版本号}<br> \- 平台:如 Android，iOS，Linux，Windows - 设备名称:如 Pixel 3，iPhone X等<br> \- 系统版本号:设备系统版本，如 2.3.3，4.2.1 等<br> \- 示例例:Android&Pixel 3&7.1;iOS&iPhone X&11.4.1
version|string|是|0.0.0.1|客户端版本号

##### （3）body请求参数
body中直接传输文件

| 名称 | 类型 | 必填 | 示例值 | 描述 |
|------|-----|-----|-----|-----|
|file | file | 是 |  |音频文件数据|


#### 4. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


### 三、返回说明
#### 1、返回参数

##### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


##### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status|	int|	0|	参照业务错误码
message|	string |	"success"|	参照业务错误码
garbage_info|	array |	[...]|	返回垃圾分类信息

garbage_info

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
garbage_name | string | 咖啡 | 垃圾名称
cate_name | string | 湿垃圾 | 垃圾分类
city_id | string | 310000 | 城市id
city_name | string | 上海市 | 城市名称
ps | string | 容器与外包装为可回收物 | 备注描述
confidence | float | 1 | 文本置信度恒为1

#### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": true,
  "remain": 4964,
  "remainTimes": 4964,
  "remainSeconds": -1,
  "msg": "查询成功,扣费",
  "result": {
    "status": 0,
    "message": "success",
    "garbage_info": [
      {
        "cate_name": "湿垃圾",
        "city_id": "310000",
        "city_name": "上海市",
        "confidence": 1.0,
        "garbage_name": "剩饭",
        "ps": "湿垃圾应从生产时就与其他品种垃圾分开收集。投放前尽量沥干水分，有外包装的应去除外包装投放"
      }
    ]
  }
}
```

#### 3、业务错误码
业务错误码（status）|对应message|说明
------|------|------
0|success|成功
4101|not enough param|缺少必要参数
4102|param error|参数有误
4301|voice data is empty|语⾳音数据为空
4302|voice too long|语⾳音数据过⻓
4303|Audio Header Format Resolution Error|音频头部格式解析错误
4304|Audio Format Error|音频格式错误
4305|Audio Sampling Rate or Channel Number Error|音频采样率或通道数错误
4107|City_id is invalid|无效的城市Id
5101|Internal Server Error|服务器内部错误

## 文本识别
### 一、接口描述

#### 1. 功能描述
提供通过文本进行垃圾分类查询的能力

#### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。


### 二、请求说明

#### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/garbageTextSearch
```

#### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/garbageTextSearch

#### 3. 请求参数

##### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
text | String | 是 | 蔬菜 |查询文本 utf8编码,仅支持简体中文输入
cityId | String | 是 | 310000 | 国家标准城市编码，请求结果根据此参数指定城市的垃圾分类标准返回，当前支持城市：310000(上海市)、330200(宁波市)、610100(西安市)、440300(深圳市)、北京市(110000)

#### 4. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


### 三、返回说明
#### 1、返回参数

##### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


##### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status|	int|	0|	参照业务错误码
message|	string |	"success"|	参照业务错误码
garbage_info|	array |	[...]|	返回垃圾分类信息

garbage_info

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
garbage_name | string | 咖啡 | 垃圾名称
cate_name | string | 湿垃圾 | 垃圾分类
city_id | string | 310000 | 城市id
city_name | string | 上海市 | 城市名称
ps | string | 容器与外包装为可回收物 | 备注描述
confidence | float | 1 | 文本置信度恒为1

#### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": true,
  "remain": 4964,
  "remainTimes": 4964,
  "remainSeconds": -1,
  "msg": "查询成功,扣费",
  "result": {
    "status": 0,
    "message": "success",
    "garbage_info": [
      {
        "cate_name": "湿垃圾",
        "city_id": "310000",
        "city_name": "上海市",
        "confidence": 1.0,
        "garbage_name": "剩饭",
        "ps": "湿垃圾应从生产时就与其他品种垃圾分开收集。投放前尽量沥干水分，有外包装的应去除外包装投放"
      }
    ]
  }
}
```
#### 3、业务错误码
业务错误码（status）|对应message|说明
------|------|------
0|success|成功
4101|not enough param|缺少必要参数
4102|param error|参数有误
4107|City_id is invalid|无效的城市Id
4108|No match result|无匹配的搜索结果
5101|Internal Server Error|服务器内部错误