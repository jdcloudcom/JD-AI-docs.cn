# 语音合成

## 一、接口描述 
### 1. 功能描述 

文字转换成语音。

### 2. 接口数据要求：
- 文本仅支持UTF-8格式。

- 文本长度不能超过1024字节。

### 3. 接口使用：

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md) 。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/tts
```

### 2. 请求方式：  
https `post` aiapi.jdcloud.com/jdai/tts

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Service-Type | string | 是 | synthesis | 服务类型，这里设置固定值synthesis
Request-Id | string | 是 | 65845428-de85-11e8-9517-040973d59a1e | 请求语音串标识码。由客户端生成，<br/>代表完整的语音识别请求过程，需要注意：<br>- 需要全局唯一<br>- 对于同一次合成请求Request-Id需要保持一致<br>- 每个不同的合成请求都要新生成Request-Id，<br/>若多次请求使用同一个将会产生不可预知的错误。<br><br>生成方法: <br>- libuuid 库可以直接生成。Android 及 iOS <br/>也有相关的生成函数。
Sequence-Id | int | 是 | 1 | 文本分段传输的分段号<br>-1表示非流式，一次性合成音频并返回。<br>1表示一次新的流式请求开始，分段合成音频返回，<br/>发送第二次请求获取第二段数据时<br/>Sequence-Id递增并可以不带text文本。
Protocol | int | 是 | 1 | 通信协议版本号，这里设置固定值1
Net-State | int | 是 | 1 | 客户端网络状态：<br/>1:WIFI，2:移动，3:联通，4:电信，5:其他
Applicator | int | 是 | 1 | 应用者，SDK 会提供给不同的应用者<br/>(渠道，例如：内部业务(0)，外部业务(1))
Property | string | 是 | {"platform": "Linux", <br/>"version": "0.0.0.1", <br/>"parameters": {<br/>"aue": "1", <br/>"vol": "2.0", <br/>"sr": "24000", <br/>"sp": "1.0", <br/>"tim": "0", <br/>"tte": "1"}} | 属性信息，json格式，platform和version为通用属性，<br/>parameters字段必填，其中的参数可选，<br/>Property允许用户同一个请求的不同包都携带该头，<br/>但是建议只在第一包携带
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名


- Property参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
platform | string | 是 | Android&Pixel&7.1 | 字符串类型，各平台的机型信息，格式为：{平台}&{机型}&{系统版本号}<br>- 平台：Android，iOS，Linux，Windows<br>- 机型：设备的机型名称，如Pixel，iPhoneX等<br>- 系统版本号：设备系统版本，如2.3.3，4.2.1等
version | string | 是 | 1.0.0 | 字符串类型，客户端版本号
parameters | string | 是 | {"aue": "1", "vol": "2.0", "sr": "24000", "sp": "1.0", "tim": "0", "tte": "1"} | TTS参数


- parameters参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
tte | int | 是 | 1 | 文本编码格式 1:UTF-8 (目前仅支持UTF-8格式)
aue | int | 是 | 1 | 音频编码格式（默认值：0）<br>0：wav	1：pcm	2：opus
tim | int | 是 | 0 | 音色（默认值：0）<br>0：女声 1：男声
vol | string | 是 | 2.0 | 音量（默认值：2.0）<br>取值范围：[0.1, 10.0]
sp | string | 是 | 1.0 | 语速（默认值：1.0）<br>取值范围：[0.5, 2.0]
sr | int | 是 | 24000 | 采样率（默认值：24000）<br>wav和pcm支持4k到24k的采样率<br>opus支持8k 12k 16k 和24k的采样率


#### （2）body请求参数
业务请求参数

类型 | 示例值 | 描述
------|-----|-----
string | 你好，京东！ | 放置要合成的文本，长度不能超过1024字节，UTF-8编码


### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数


名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | ok | 参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 65845428-de85-11e8-9517-040973d59a1e | 便于双方定位问题（与请求头部的request-id一致）
index | int | -3 | 分段序号，从1开始，负值表示最后一包（非流式直接返回-1）
audio | string | Uv4I/mD+zf4… | 音频数据（base64编码）


### 2、返回示例  

```
{
    "code": "10000",
    "charge": false,
    "remain": 0,
    "msg": "查询成功",
    "result": {
        "status": 0,
        "message": "ok",
        "request_id": "65845428-de85-11e8-9517-040973d59a1e",
        "index": -3,
        "audio": "Uv4I/mD+zf4…"
    }
}
```



​	


