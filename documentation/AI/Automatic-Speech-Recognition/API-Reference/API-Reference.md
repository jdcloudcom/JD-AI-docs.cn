# 语音识别

## 一、接口描述 

### 1. 功能描述
语音转换成文字。

### 2. 能力说明
语音识别API根据不同的使用场景，使用在对应领域场景下训练的模型，以提高识别准确率。

### 3. 音频要求
> 1. 建议的音频格式：wav、mp3、amr
> 2. 建议的音频采样率：8000 Hz 或 16000 KHz（根据模型领域选择）
> 3. 建议的声道数：单声道
> 4. 单次请求的音频最大时长：60秒以内

### 4. 接口使用
在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md) 。

## 二、请求说明

### 1. 接口地址

```
https://aiapi.jdcloud.com/jdai/asr
```

### 2. 请求方式
https `post` aiapi.jdcloud.com/jdai/asr


### 3. 请求参数

#### （1）header请求参数  

- 字段说明：

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Domain | string | 是 | search | 模型领域：<br>- general，通用场景，需要使用 16000 Hz 采样率的音频<br>- call_center，呼叫中心场景，需要使用 8000 Hz 采样率的音频
Application-Id | string | 否 | your Application-Id | 产品ID：<br>- 业务方应用名称，由业务方在客户端自行生成。
Request-Id | string | 是 | *56a847e6-84c0-4c01-bf4b-d566f2d2dd11 | 请求 ID：<br>- *注意：示例值仅供参考，正式使用请务必通过 uuid 生成<br>- 对于同一次请求 Request-Id 需要保持一致，多次请求使用同一个将会产生不可预知的错误
Sequence-Id | int | 是 | -1 | 语音传输分段号：<br>- 从 1 开始依次递增，最后一段语音取负值，分为下述两种情况：<br>1. 在一个 Request-Id 中，上传整个音频文件（整包请求）时：填 -1<br>2. 在一个 Request-Id 中，音频文件分段上传（分段请求）时，遵循默认规则依次递增。例如：一次语音识别请求中，音频分 10 次上传，则 Sequence-Id 依次为：1,2,3,4,5,6,7,8,9,-10
Asr-Protocol | int | 是 | 1 | 通信协议版本号：<br>- 默认填 1
Net-State | int | 否 | 2 | 客户端网络状态：<br>- NETSTATE_NO_NETWORK = 0;<br>- NETSTATE_NO_WIFI_MOBILE = 1; <br>- NETSTATE_WIFI = 2; <br>- NETSTATE_CDMA = 3; <br>- NETSTATE_EDGE = 4;   //移动 2.5G<br>- NETSTATE_EVDO_0 =5; <br>- NETSTATE_EVDO_A = 6; <br>- NETSTATE_GPRS = 7; <br>- NETSTATE_HSDPA = 8;   //联通 3G<br>- NETSTATE_HSPA = 9;<br>- NETSTATE_HSUPA = 10;<br>- NETSTATE_UMTS = 11;<br>- NETSTATE_EHRPD = 12;<br>- NETSTATE_EVDO_B = 13;<br>- NETSTATE_HSPAP = 14;<br>- NETSTATE_IDEN = 15;<br>- NETSTATE_LTE = 16;<br>- NETSTATE_UNKOWN_MOBILE = 20;
Applicator | int | 否 | 1 | 业务方信息：<br>- 0：内部业务方<br>- 1：外部业务方</td>
Property | JSON | 是 | {...} | 语音识别请求参数：<br>- 注意：如果 Sequence-Id 为 1 或 -1 时，则 Property 参数必填；其他情况下，该参数可选填</td>


- Property参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
autoend | bool | 是 | false | 服务端自动断尾检测（VAD）功能开关：<br>- false：不开启 VAD 功能<br>- true：开启 VAD 功能
platform | string | 是 | Linux&Centos&7.3 | 平台信息：<br>格式：{系统信息}&{设备信息}&{系统版本号}<br>- 系统信息：如 Android，iOS，Linux，Windows<br>- 设备信息：如 Pixel 3，iPhone X 等<br>- 系统版本号：设备系统版本，如 2.3.3，4.2.1 等<br>- 示例：Android&Pixel 3&7.1；iOS&iPhone X&11.4.1
version | string | 是 | 0.0.0.1 | 客户端版本号
encode | JSON | 是 | {...} | 音频参数

- encode字段

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
channel | int | 是 | 1 | 音频声道数：<br>- 建议使用单声道音频，单声道填 1
format | string | 是 | wav | 音频格式：<br>- 建议使用 wav，amr，mp3 格式
sample_rate | int | 是 | 16000 | 音频采样率：<br>- 通用场景使用 16000 Hz，填 16000<br>- 呼叫中心场景使用 8000 Hz，填 8000
post_process | int | 否 | 0 | 数字后处理：<br>- 0：根据服务端配置是否进行数字后处理<br>- 1：强制开启数字后处理（开启后，会把结果中的数字汉字转换成阿拉伯数字。例如，识别结果中的"一千"会转成"1000"）

#### （2）body请求参数
填充待识别的音频数据（二进制）。
音频数据可按照自定义长度进行切分，按顺序分包上传，并与 header 请求参数中的 Sequence-Id 参数的顺序保持对应。

### 4. 请求代码示例

建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

Python 3 示例程序如下：

```python
import requests
import json
import time
import uuid
import hashlib
from urllib.parse import urlencode
import sys
import importlib
importlib.reload(sys)

url = 'https://aiapi.jd.com/jdai/asr'

encode = {
	'channel':1,
	'format':'wav',
	'sample_rate':16000,
	}
Property = {
	'platform':'Linux',
	'version':'0.0.0.1',
	'autoend':False,
	'encode':encode,
	}
headers = {
	'Content-Type':'application/octet-stream',
	'Domain':'general',
	'Request-Id':str(uuid.uuid1()),
	'Sequence-Id':str(-1),
	'Property':json.dumps(Property)
	}
query = {
	'appkey':'your appkey',
	'timestamp':'',
	'sign':''
	}

audiofile = '16k_audio.wav'
secretkey = 'your secretkey'

def test_single(audiofile):
  query['timestamp'],query['sign'] = sign(secretkey)
  url_query = '?'.join([url, urlencode(query)])
  #seq = 1
  #packagelen = 4000
  
  with open(audiofile, mode='rb') as f:
    while True:
      audiodata=f.read()
      #audiodata=f.read(int(packagelen))
      if not audiodata:
        break
      #else:
        #if len(audiodata) < int(packagelen):
          #headers['Sequence-Id'] = str(-seq)
        #else:
          #headers['Sequence-Id'] = str(seq)
      r = requests.post(url_query, headers=headers, data=audiodata)
      #seq += 1
  print(r.text)

def sign(secretkey):
    m = hashlib.md5()
    nowTime = int(time.time() * 1000)
    before = secretkey + str(nowTime)
    m.update(before.encode('utf8'))
    return str(nowTime), m.hexdigest()

if __name__ == '__main__':
    audiofile = sys.argv[1] if len(sys.argv) > 1 else audiofile
    test_single(audiofile)
```

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

```JSON
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