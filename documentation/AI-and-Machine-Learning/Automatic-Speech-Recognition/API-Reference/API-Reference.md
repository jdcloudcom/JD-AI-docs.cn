# 语音识别

## 一、接口描述 

### 1. 功能描述
语音转换成文字。

### 2. 能力说明
语音识别API根据不同的使用场景，使用在对应领域场景下训练的模型，以提高识别准确率。

### 3. 音频要求
> 1. 目前支持的音频格式：wav、mp3、amr
> 2. 目前支持的采样率：16000
> 3. 一次请求的音频最大时长：60秒

### 4. 接口使用
公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK参照[接口鉴权](../Operation-Guide/Authentication.md) 规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md) 。

## 二、请求说明

### 1. 接口地址

```
https://aiapi.jdcloud.com/jdai/asr
```

### 2. 请求方式
https `post` aiapi.jdcloud.com/jdai/asr


### 3. 请求参数

#### （1）header请求参数  

- 示例：

```Json
{
	"Domain":"search",
	"Application-Id":"JD-logistics-app",
	"Request-Id":"56a847e6-84c0-4c01-bf4b-d566f2d2dd11",
	"Sequence-Id":1,
	"Asr-Protocol":1,
	"Net-State":2,
	"Applicator":0,
	"Property":{
		"autoend" : false, 
		"encode" : {
			"channel" : 1, 
			"format" : "wav", 
			"sample_rate" : 16000
		},
		"platform" : "Linux", 
		"version" : "0.0.0.1"
	}
}
```
- 字段说明：

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Domain | string | 是 | search | 领域。跟语音识别场景有关，目前可选值为：<br>- search<br>- jingme_mia
Application-Id | string | 是 | search-app | 产品ID。业务方应用名称，由Client端生成。
Request-Id | string | 是 | 56a847e6-84c0-4c01-bf4b-d566f2d2dd11-app | 请求语音串标识码。由客户端生成，<br/>代表完整的语音识别请求过程，需要注意：<br>- 需要全局唯一<br>- 对于同一次请求Request-Id需要保持一致<br>- 每一次识别请求都要新生成Request-Id，<br/>若多次请求使用同一个将会产生不可预知的错误。<br><br>生成方法: <br>- libuuid 库可以直接生成。Android 及 iOS也有相关的生成函数。
Sequence-Id | int | 是 | -1 | 语音分段传输的分段号。从 1 开始，为负表示最后一段语音。<br/>例如：一次语音识别请求分10个请求，<br/>则Sequence-Id依次为：1,2,3,4,5,6,7,8,9,-10
Asr-Protocol | int | 是 | 1 | 通信协议版本号，使用 1 即可
Net-State | int | 是 | 2 | 客户端网络状态：<br>- NETSTATE_NO_NETWORK = 0;<br>- NETSTATE_NO_WIFI_MOBILE = 1; <br>- NETSTATE_WIFI = 2; <br>- NETSTATE_CDMA = 3; <br>- NETSTATE_EDGE = 4;   //移动 2.5G<br>- NETSTATE_EVDO_0 =5; <br>- NETSTATE_EVDO_A = 6; <br>- NETSTATE_GPRS = 7; <br>- NETSTATE_HSDPA = 8;   //联通 3G<br>- NETSTATE_HSPA = 9;<br>- NETSTATE_HSUPA = 10;<br>- NETSTATE_UMTS = 11;<br>- NETSTATE_EHRPD = 12;<br>- NETSTATE_EVDO_B = 13;<br>- NETSTATE_HSPAP = 14;<br>- NETSTATE_IDEN = 15;<br>- NETSTATE_LTE = 16;<br>- NETSTATE_UNKOWN_MOBILE = 20;
Applicator | int | 是 | 1 | 应用者，SDK 会提供给不同的应用者<br/>(渠道，例如：内部业务(0)，外部业务(1))</td>
*Property | bject | 否 | {...} | 包含语音识别相关的请求参数<br/>(如果请求的音频不分包上传，请求时该参数必填；如果分包上传，则第一次请求必填，后边的请求可选)<br/>例如采样率、音频格式等。此参数要在第一个请求包的时候传过来，即Sequence-Id为 1 或者 -1 (-1 表示一次语音识别请求只有一个http请求包的情况)
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名


- Property参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
autoend | bool | 是 | false | bool类型，是否开启服务端自动断尾，即服务端vad，默认填false
encode | object | 是 | {...} | 语音识别的请求格式：<br>- channel：int类型，音频声道数，目前只支持单声道，填1<br>- format：string类型，音频格式，目前支持wav，amr，mp3<br>- sample_rate：int类型，采样率，目前只支持16000
platform | string | 是 | iOS&iPhoneX&11.4.1 | 字符串类型，各平台的机型信息，格式为：{平台}&{机型}&{系统版本号}<br>- 平台：Android，iOS，Linux，Windows<br>- 机型：设备的机型名称，如Pixel，iPhoneX等<br>- 系统版本号：设备系统版本，如2.3.3，4.2.1等<br>- 示例：Android&Pixel&7.1；iOS&iPhoneX&11.4.1
version | string | 是 | 0.0.0.1 | 客户端版本号

#### （2）body请求参数
放置待识别的语音数据。数据可根据语音切分，按序上传，跟Header中Sequence-Id的顺序保持对应。

### 4. 请求代码示例

建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


## 三、返回说明 

### 1. 返回参数

#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数

服务器返回的识别结果采用json格式：

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
request_id | string | 56a847e6-84c0-4c01-bf4b-d566f2d2dd11 | 请求id
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
index | int | -1 | 返回结果编号，负数表示全部最终结果
message | string | 语音数据为空 | 参见[错误码](Error-Code.md)-业务级错误码
content | object | {...} | 识别结果

### 2. 返回示例

```Json
{
    "code": "10000",
    "charge": false,
    "remain": 0,
    "msg": "查询成功",
    "result": {
        "request_id": "56a847e6-84c0-4c01-bf4b-d566f2d2dd11",
        "status": 0,
        "index": -1,
        "message": "",
        "content": [
            {
                "text": "你好 京东"
            }
        ]
    }
}
```