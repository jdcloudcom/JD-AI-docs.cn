# 声纹识别

## 一、接口描述

### 1. 功能描述
> 声纹识别基于说话人的声音提供说话人确认功能。

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明

> 声纹识别API提供说话人注册以及说话人确认的功能。用户可以先用声音进行注册，再根据声音进行说话人确认。

### 4. 音频要求

> 1. 目前支持的音频格式为：wav、mp3、amr
> 2. 音频采样率为：16 KHz
> 3. 音频通道数：单通道
> 4. 一次请求的音频最大时长：60 秒

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/vpr
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/vpr

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）query请求参数

<table>
  <tr>
    <th>名称</th>
    <th>类型</th>
    <th>必填</th>
    <th>示例值</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>Content-Type</td>
    <td>string</td>
    <td>是</td>
    <td>application/octet-stream</td>
    <td>内容类型:
        <br>不可用的Content-Type：
        <br>- multipart/form-data
        <br>- application/x-www-form-urlencoded
  </tr>
  <tr>
    <td>Application-Id</td>
    <td>string</td>
    <td>否</td>
    <td>your Application-Id</td>
    <td>产品 ID：
        <br>- 业务方应用名称，由业务方在客户端自行生成</td>
  </tr>
  <tr>
    <td>Request-Id</td>
    <td>string</td>
    <td>是</td>
    <td>*56a847e6-84c0-4c01-bf4b-d566f2d2dd11</td>
    <td>请求ID：
    <br>- *注意：示例值仅供参考，正式使用请务必通过 uuid 生成
    <br>- 对于同一次请求 Request-Id 需要保持一致，多次请求使用同一个将会产生不可预知的错误</td>
  </tr>
  <tr>
    <td>User-Id</td>
    <td>string</td>
    <td>是</td>
    <td>IMEI-12345678</td>
    <td>用户ID：
    <br>- *注意：示例值仅供参考
    <br>- 用户id是某一个人唯一的身份id</td>
  </tr>
  <tr>
    <td>Sequence-Id</td>
    <td>int</td>
    <td>是</td>
    <td>-1</td>
    <td>语音传输分段号：
        <br>- 从 1 开始依次递增，最后一段语音取负值，分为下述两种情况：
    	<br>1. 在一个 Request-Id 中，上传整个音频文件（整包请求）时：填 -1
    	<br>2. 在一个 Request-Id 中，音频文件分段上传（流式分包请求）时，遵循默认规则依次递增。例如：一次语音识别请求中，音频分 10 次上传，则 Sequence-Id 依次为：1,2,3,4,5,6,7,8,9,-10</td>
  </tr>
  <tr>
    <td>Server-Protocol</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>通信协议版本号：
        <br>- 默认填 1</td>
  </tr>
  <tr>
    <td>Net-State</td>
    <td>int</td>
    <td>是</td>
    <td>2</td>
    <td>客户端网络状态：
    <br>- NETSTATE_NO_NETWORK = 0;
    <br>- NETSTATE_NO_WIFI_MOBILE = 1;
    <br>- NETSTATE_WIFI = 2;
    <br>- NETSTATE_CDMA = 3;
    <br>- NETSTATE_EDGE = 4;   //移动 2.5G
    <br>- NETSTATE_EVDO_0 =5;
    <br>- NETSTATE_EVDO_A = 6;
    <br>- NETSTATE_GPRS = 7;
    <br>- NETSTATE_HSDPA = 8;   //联通 3G
    <br>- NETSTATE_HSPA = 9;
    <br>- NETSTATE_HSUPA = 10;
    <br>- NETSTATE_UMTS = 11;
    <br>- NETSTATE_EHRPD = 12;
    <br>- NETSTATE_EVDO_B = 13;
    <br>- NETSTATE_HSPAP = 14;
    <br>- NETSTATE_IDEN = 15;
    <br>- NETSTATE_LTE = 16;
    <br>- NETSTATE_UNKOWN_MOBILE = 20;</td>
  </tr>
  <tr>
    <td>Applicator</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>业务方信息：
    <br>- 0：内部业务方
    <br>- 1：外部业务方</td>
  </tr>
  <tr>
    <td>Property</td>
    <td>JSON</td>
    <td>否</td>
    <td>{...}</td>
    <td>语音识别请求参数：
    <br>- 注意：如果 Sequence-Id 为 1 或 -1 时，则 Property 参数必须要填；其他情况下，该参数可选填</td>
  </tr>
</table>

- Property 字段

<table>
  <tr>
    <th>名称</th>
    <th>类型</th>
    <th>必填</th>
    <th>示例值</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>autoend</td>
    <td>bool</td>
    <td>是</td>
    <td>false</td>
    <td>服务端自动断尾检测（VAD）功能开关：
        <br>- false：不开启 VAD 功能
        <br>- true：开启 VAD 功能</td>
  </tr>
  <tr>
    <td>platform</td>
    <td>string</td>
    <td>是</td>
    <td>Linux&Centos&7.3</td>
    <td>平台信息：
     <br>格式：{系统信息}&{设备信息}&{系统版本号}
     <br>- 系统信息：如 Android，iOS，Linux，Windows
     <br>- 设备信息：如 Pixel 3，iPhone X 等
     <br>- 系统版本号：设备系统版本，如 2.3.3，4.2.1 等
     <br>- 示例：Android&Pixel 3&7.1；iOS&iPhone X&11.4.1</td>
  </tr>
  <tr>
    <td>version</td>
    <td>string</td>
    <td>是</td>
    <td>0.0.0.1</td>
    <td>客户端版本信息</td>
  </tr>
  <tr>
    <td>vpr_mode</td>
    <td>string</td>
    <td>是</td>
    <td>enroll</td>
    <td>表示本次请求是注册还是说话人确认，取值为enroll, test。注册时设为enroll， 说话人确认时设为test。
    	<br>-注：需要先注册两遍声纹，才能进行说话人确认。
    </td>
  </tr>
  <tr>
    <td>encode</td>
    <td>JSON</td>
    <td>是</td>
    <td>{...}</td>
    <td>音频参数</td>
  </tr>
 </table>

- encode 字段

<table>
  <tr>
    <th>名称</th>
    <th>类型</th>
    <th>必填</th>
    <th>示例值</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>channel</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>音频声道数：
        <br>- 目前只支持单声道，填 1</td>
  </tr>
  <tr>
    <td>format</td>
    <td>string</td>
    <td>是</td>
    <td>wav</td>
    <td>音频声道数：
        <br>- 目前支持 wav，amr，mp3 格式</td>
  </tr>
  <tr>
    <td>sample_rate</td>
    <td>int</td>
    <td>是</td>
    <td>16000</td>
    <td>音频采样率：
        <br>- 目前只支持16KHz，填 16000</td>
  </tr>
</table>

#### （3）body请求参数

填充待识别的音频数据（二进制）。
音频数据可按照自定义长度进行切分，按顺序分包上传，并与 header 请求参数中的 Sequence-Id 参数的顺序保持对应。

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
服务器返回的识别结果采用 JSON 格式：

<table>
  <tr>
    <th>名称</th>
    <th>类型</th>
    <th>示例值</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>request_id</td>
    <td>string</td>
    <td>56a847e6-84c0-4c01-bf4b-d566f2d2dd11</td>
    <td>请求ID</td>
  </tr>
  <tr>
    <td>status</td>
    <td>int</td>
    <td>0</td>
    <td>状态码</td>
  </tr>
  <tr>
    <td>index</td>
    <td>int</td>
    <td>-1</td>
    <td>返回结果编号，负数表示全部最终结果</td>
  </tr>
  <tr>
    <td>message</td>
    <td>string</td>
    <td>语音数据为空</td>
    <td>错误信息（返回正常时该字段的值为空）</td>
  </tr>
  <tr>
    <td>result</td>
    <td>JSON</td>
    <td>{...}</td>
    <td>识别结果，其中包含text对象，其值可取以下几个值：
    not_enrolled(尚未注册),
    <br>enrolling(注册中),
    <br>enrlled(注册完成),
    <br>reject(验证失败),
    <br>accept(验证通过)</td>
  </tr>
</table>

### 2、返回示例

```JSON
{
    "code": "10000",
    "charge": false,
    "remainTimes": 4998,
    "remainSeconds": -1,
    "msg": "查询成功",
    "result": {
        "request_id": "56a847e6-84c0-4c01-bf4b-d566f2d2dd11",
        "status": 0,
        "index": -1,
        "message": "",
        "result": [
            {
                "text": "accept"
            }
        ]
    }
}
```

### 3、业务错误码
<table>
  <tr>
    <th>业务错误码（status）</th>
    <th>message</th>
    <th>说明</th>
  </tr>
  <tr>
    <td>61001</td>
    <td>speech data is empty.</td>
    <td>语音数据为空</td>
  </tr>
  <tr>
    <td>61002</td>
    <td>speech data is too long.</td>
    <td>语音数据过长，一次请求音频不能超过一分钟</td>
  </tr>
   <tr>
    <td>61003</td>
    <td>request params error.</td>
    <td>请求参数出错，缺少 Request-Id、Sequence-Id 或 Application-Id 等。</td>
  </tr>
   <tr>
    <td>61004</td>
    <td>speech data file header error.</td>
    <td>音频头部格式解析错误</td>
  </tr>
   <tr>
    <td>61005</td>
    <td>speech sample rate or channel error.</td>
    <td>音频采样率或通道数错误</td>
  </tr>
   <tr>
    <td>61006</td>
    <td>speech format error.</td>
    <td>音频格式错误</td>
  </tr>
   <tr>
    <td>62001</td>
    <td>codec error.</td>
    <td>服务内部音频解码错误</td>
  </tr>
   <tr>
    <td>62002</td>
    <td>am server internal error.</td>
    <td>服务内部am-server模块错误</td>
  </tr>
  <tr>
    <td>62003</td>
    <td>connect to decoder server error.</td>
    <td>服务内部链接engine-server模块错误</td>
  </tr>
   <tr>
    <td>63001</td>
    <td>vpr userid too long.</td>
    <td>注册用户名过长</td>
  </tr>
   <tr>
    <td>63002</td>
    <td>vpr mode error.</td>
    <td>不支持的声纹模式</td>
  </tr>
   <tr>
    <td>63003</td>
    <td>vpr audio too short.</td>
    <td>音频文件过短</td>
  </tr>
   <tr>
    <td>63004</td>
    <td>vpr not enrolled.</td>
    <td>该用户尚未注册声纹</td>
  </tr>
   <tr>
    <td>63005</td>
    <td>vpr other error.</td>
    <td>服务内部其他错误</td>
  </tr>
   <tr>
    <td>63007</td>
    <td>vpr other request enrolling or testing this userid.</td>
    <td>该用户id正在被其他请求进行声纹注册或声纹认证</td>
  </tr>
   <tr>
    <td>63009</td>
    <td>vpr reqid is invalidation.</td>
    <td>该请求已失效</td>
</table>