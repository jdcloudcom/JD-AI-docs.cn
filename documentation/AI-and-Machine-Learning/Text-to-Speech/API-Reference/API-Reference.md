# 语音合成
## 一、接口描述 
### 1. 功能描述 
文字转换成语音。
### 2. 接口数据要求：
- 文本仅支持UTF-8格式。

- 文本长度不能超过1024字节。

### 3. 接口使用：

公测期间用户可以免费（0元）进行测试，根据[购买流程](http://neuhub.jd.com/ai/api/nlp/classification)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](https://aidoc.jd.com/user/auth.html)规则进行相应开发，整体流程详见   [接入流程](https://aidoc.jd.com/user/flow.html) 。

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
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>Service-Type</td>
      <td>string</td>
      <td>是</td>
      <td>synthesis</td>
      <td>服务类型，这里设置固定值synthesis</td>
   <tr>
      <td>Request-Id</td>
      <td>string</td>
      <td>是</td>
      <td>65845428-de85-11e8-9517-040973d59a1e</td>
     <td>请求语音串标识码。由客户端生成，代表完整的语音识别请求过程，需要注意：
    <br>- 需要全局唯一
    <br>- 对于同一次合成请求Request-Id需要保持一致
    <br>- 每个不同的合成请求都要新生成Request-Id，若多次请求使用同一个将会产生不可预知的错误。<br><br>生成方法: 
	 <br>- libuuid 库可以直接生成。Android 及 iOS 也有相关的生成函数。</td>
   </tr>
      <tr>
    <td>Sequence-Id</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>文本分段传输的分段号
      <br>-1表示非流式，一次性合成音频并返回。
      <br>1表示一次新的流式请求开始，分段合成音频返回，发送第二次请求获取第二段数据时Sequence-Id递增并可以不带text文本。</td>
  </tr>
  <tr>
    <td>Protocol</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>通信协议版本号，这里设置固定值1</td>
  </tr>
  <tr>
    <td>Net-State</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>客户端网络状态：1:WIFI，2:移动，3:联通，4:电信，5:其他</td>
  </tr>
  <tr>
    <td>Applicator</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>应用者，SDK 会提供给不同的应用者(渠道，例如：内部业务(0)，外部业务(1))</td>
  </tr>
  <tr>
    <td>Property</td>
    <td>string</td>
    <td>是</td>
    <td>{"platform": "Linux", "version": "0.0.0.1", "parameters": {"aue": "1", "vol": "2.0", "sr": "24000", "sp": "1.0", "tim": "0", "tte": "1"}}</td>
    <td>属性信息，json格式，platform和version为通用属性，parameters字段必填，其中的参数可选，Property允许用户同一个请求的不同包都携带该头，但是建议只在第一包携带</td>
  </tr>
   <tr>
      <td>Authorization</td>
      <td>string</td>
      <td>是</td>
      <td>JDCLOUD2-HMAC-SHA256Credential=access...</td>
      <td>签名</td>
   </tr>
</table>

- Property参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
    <td>platform</td>
    <td>string</td>
    <td>是</td>
    <td>Android&Pixel&7.1</td>
    <td>字符串类型，各平台的机型信息，格式为：{平台}&{机型}&{系统版本号}
	 <br>- 平台：Android，iOS，Linux，Windows
	 <br>- 机型：设备的机型名称，如Pixel，iPhoneX等
	 <br>- 系统版本号：设备系统版本，如2.3.3，4.2.1等</td>
  </tr>
  <tr>
    <td>version</td>
    <td>string</td>
    <td>是</td>
    <td>1.0.0</td>
    <td>字符串类型，客户端版本号</td>
  </tr>
  <tr>
    <td>parameters</td>
    <td>string</td>
    <td>是</td>
    <td>{"aue": "1", "vol": "2.0", "sr": "24000", "sp": "1.0", "tim": "0", "tte": "1"}</td>
    <td>TTS参数</td>
  </tr>
   <tr>
</table>

- parameters参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
  <tr>
    <td>tte</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>文本编码格式 1:UTF-8 (目前仅支持UTF-8格式)</td>
  </tr>
  <tr>
    <td>aue</td>
    <td>int</td>
    <td>是</td>
    <td>1</td>
    <td>音频编码格式（默认值：0）
      <br>0：wav	1：pcm	2：opus</td>
  </tr>
  <tr>
    <td>tim</td>
    <td>int</td>
    <td>是</td>
    <td>0</td>
    <td>音色（默认值：0）
      <br>0：女声 1：男声</td>
  </tr>
  <tr>
    <td>vol</td>
    <td>string</td>
    <td>是</td>
    <td>2.0</td>
    <td>音量（默认值：2.0）
      <br>取值范围：[0.1, 10.0]</td>
  </tr>
  <tr>
    <td>sp</td>
    <td>string</td>
    <td>是</td>
    <td>1.0</td>
    <td>语速（默认值：1.0）
      <br>取值范围：[0.5, 2.0]</td>
  </tr>
  <tr>
    <td>sr</td>
    <td>int</td>
    <td>是</td>
    <td>24000</td>
    <td>采样率（默认值：24000）
      <br>wav和pcm支持4k到24k的采样率
	  <br>opus支持8k 12k 16k 和24k的采样率</td>
  </tr>
</table>

#### （2）body请求参数
业务请求参数
<table>
   <tr>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>string</td>
      <td>你好，京东！</td>
      <td>放置要合成的文本，长度不能超过1024字节，UTF-8编码</td>
   </tr>
</table>

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](未发布)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>code</td>
      <td>string</td>
      <td>1000</td>
      <td>参见下方错误码-系统级错误码</td>
   </tr>
      <tr>
      <td>charge</td>
      <td>boolean</td>
      <td>false 或 true</td>
      <td>false：不扣费， true：扣费</td>
   </tr>
      <tr>
      <td>remain</td>
      <td>long</td>
      <td>1305</td>
      <td>按天计算剩余调用次数</td>
   </tr>
      </tr>
      <tr>
      <td>msg</td>
      <td>string</td>
      <td>查询成功</td>
      <td>参见下方错误码-系统级错误码数</td>
   </tr>
      </tr>
      <tr>
      <td>result</td>
      <td>object</td>
      <td>{...}</td>
      <td>查询结果</td>
   </tr>
</table>

#### （2）业务返回参数
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>status</td>
      <td>int</td>
      <td>0</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
      <tr>
      <td>message</td>
      <td>string</td>
      <td>ok</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
      <tr>
      <td>request_id</td>
      <td>string</td>
      <td>65845428-de85-11e8-9517-040973d59a1e</td>
      <td>便于双方定位问题（与请求头部的request-id一致）</td>
   </tr>
   <tr>
      <td>index</td>
      <td>int</td>
      <td>-3</td>
      <td>分段序号，从1开始，负值表示最后一包（非流式直接返回-1）</td>
   </tr>
   <tr>
      <td>audio</td>
      <td>string</td>
      <td>Uv4I/mD+zf4…</td>
      <td>音频数据（base64编码）</td>
   </tr>
</table>

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


