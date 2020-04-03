# 行人重识别

## 一、接口描述

### 1. 功能描述
> 行人重识别API能够根据图片中一个行人的服饰，肤色，身高，体态等人体特点，提取行人的特征，返回其特征矩阵。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明

> 输入图片中人像占整张图的比例应尽量大。人像的矩形框边长建议不小于图片最短边边长的 1 / 2。例如图片为 1080*960 像素，则建议的最小人体框最短边尺寸为 480 像素。如果不满足此要求，则可能会影响识别精度。建议配合人体检测api使用。

### 4. 音频要求

- 图片格式：jpg、jpeg、png、jfif
- 图片像素尺寸：最小 256\*256 像素，最大 4096\*4096 像素
- 图片文件大小：小于2M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/personreid
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/personreid

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）query请求参数

#### （3）body请求参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>无</td>
      <td>binary</td>
      <td>必选</td>
      <td>采用二进制方式读取图片</td>
      <td>图片内容，传入图片</td>
   </tr>
</table>

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
      <td>status</td>
      <td>int</td>
      <td>0</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
   <tr>
      <td>message</td>
      <td>string</td>
      <td>OK</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
   <tr>
      <td>request_id</td>
      <td>string</td>
      <td>12345678</td>
      <td>便于双方定位问题</td>
   </tr>
   <tr>
      <td>used_time</td>
      <td>int</td>
      <td>198</td>
      <td>整个请求花费的时间，单位为毫秒</td>
   </tr>
   <tr>
      <td>humanDetectionResult</td>
      <td>array</td>
      <td>[[x1,y1,x2,y2,score],[x1,y1,x2,y2,score],...]</td>
      <td>x1,y1,x2,y2,score分别表示预测出的人体矩形框的左上角坐标，右下角坐标，以及置信度。返归的矩形框按照置信度高低排序，当未检测到人体时，返回空array[]。</td>
   </tr>
   <tr>
      <td>personreidResult</td>
      <td>array</td>
      <td> [[0.031304, 0.410153, …]]  </td>
      <td>返回的特征矩阵按照humanDetectionResult中所框出的图片的置信度高低进行排序。矩阵中特征矩阵的数量与humanDetectionResult中返回矩阵框的数量一致，当未检测到人体时，返回空array[]，每个特征矩阵为一个2048维的人体特征矩阵。根据此特征矩阵与其他行人的特征矩阵做余弦距离对比可以得到相似度 </td>
   </tr>
</table>

### 2、返回示例

```JSON
{
    "code": 10000,
    "charge": false,
    "remainTimes": 4998,
    "remainSeconds": -1,
    "msg": "查询成功",
    "result":
    {
        "status":0,
        "request_id": "1544940159.6349967",
        "message":"ok",
        "used_time":40,
        "humanDetectionResult":[
            [265, 127, 314, 261, 0.96]
        ],
        "personreidResult":
        [
            [0.0313025526702404, 0.41015300154685974, 0.38227754831314087, 0.0668988972902298, 0.30472421646118164,…]
        ]
    }
}

```

### 3、业务错误码
<table>
   <tr>
      <th>业务错误码（status）</th>
      <th>message</th>
      <th>说明 </th>
   </tr>
   <tr>
      <td>12002</td>
      <td>not enough param</td>
      <td>参数缺失，未传入图片 </td>
   </tr>
   <tr>
      <td>12003</td>
      <td>image type error</td>
      <td>解析参数错误,图片格式不支持</td>
   </tr>
    <tr>
      <td>12004</td>
      <td>image size must be between 256X256 and 4096X4096</td>
      <td>图片大小超过限制</td>
   </tr>
   <tr>
      <td>12004</td>
      <td>image size exceeds 2M</td>
      <td>图片大小超过限制，图片尺寸不在支持范围内，与上方情况共用一个错误码</td>
   </tr>
      <tr>
      <td>12005</td>
      <td>image has no person</td>
      <td>图片没有检测到人</td>
   </tr>
</table>