#人脸活体检测

## 一、接口描述 

### 1.功能描述

人脸活体检测API主要用于针对用户上传图像，返回该图像中的人脸是否为真人
单目可见光防伪结构：1、适用场景：移动设备前置摄像头；2、安全等级：中，建议使用在对安全等级要求并不高的应用场景；3、测试流程：建议对真人以及hack两种case分别进行测试，即测试真人的通过率以及hack的检出率。

### 2. 接口使用 

使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3.图片要求

> 1. 图片格式：bmp, jpg, jpeg, png, jfif
> 2. 图片像素尺寸：最小 48\*48 像素，最大 2048\*2048 像素
> 3. 图片 Base64 大小：小于2MB

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/detectHacknessV1
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/detectHacknessV1

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名


#### （2）body请求参数
业务请求参数
<table>
   <tr>
      <td>名称</td>
      <td>类型</td>
      <td>必填</td>
      <td>示例值</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>isVisual</td>
      <td>bool</td>
      <td>是</td>
      <td>true</td>
      <td>true：可见光 单张图片防伪，需要提供 imgBase64Visual；false：可见光 + 近红外 两张图片防伪，需要提供 imgBase64Visual、imgBase64Nir</td>
   </tr>
   <tr>
      <td>imgBase64Visual</td>
      <td>string</td>
      <td>是</td>
      <td>图像Base64编码值，去掉图片头"data:image/png;base64,"，imgBase64Visual=iVBORw0K...（由于过长，不给出示例）</td>
      <td>可见光图片Base64编码</td>
   </tr>
   <tr>
      <td>imgBase64Nir</td>
      <td>string</td>
      <td>是/否</td>
      <td>图像Base64编码值，去掉图片头"data:image/png;base64,"，imgBase64Nir=iVBORw0K...（由于过长，不给出示例）</td>
      <td>近红外图片Base64编码</td>
   </tr>
</table>

### 4. 请求代码示例
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
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>code</td>
      <td>int</td>
      <td>0</td>
      <td>状态码，0 为成功，非 0 请参考以下 业务错误码</td>
   </tr>
   <tr>
      <td>msg</td>
      <td>string</td>
      <td>Accept</td>
      <td>状态码对应的说明</td>
   </tr>
   <tr>
      <td>processTimeInMs</td>
      <td>long</td>
      <td>34</td>
      <td>从接收请求到处理结束的耗时，毫秒</td>
   </tr>
   <tr>
      <td>timestamp</td>
      <td>long</td>
      <td>1576728627956</td>
      <td>返回时的时间戳</td>
   </tr>
   <tr>
      <td>score</td>
      <td>float</td>
      <td>0.009</td>
      <td>假体分数，严格的阈值为0.2，小于0.2为假体，正常的阈值为0.38，小于0.38为假体</td>
   </tr>
   <tr>
      <td>faceItemsVisual</td>
      <td>array</td>
      <td>[]</td>
      <td>每个人脸的检测结果；具体类型请参考下方</td>
   </tr>
</table>

**faceItems 数组中单个元素的结构：**
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>boundingBox</td>
      <td>object</td>
      <td>{
				"left" : 490.11,
				"top" : 85.42,
				"width" : 108.84,
				"height" : 143.84
			}</td>
      <td>人脸识别矩形框的位置，包括以下属性值：<br/>
      left：矩形框左上角像素点的横坐标<br/>
      top：矩形框左上角像素点的纵坐标<br/>
      width：矩形框的宽度<br/>
      height：矩形框的高度</td>
   </tr>
   <tr>
      <td>posture</td>
      <td>object</td>
      <td>{
				"yaw" : -11.58,
				"pitch" : -4.56,
				"roll" : -2.37
			}</td>
      <td>人脸角度，包括以下属性值：<br/>
      yaw：人脸旋转角度，偏航角（Y轴），单位 度<br/>
      pitch：人脸旋转角度，俯仰角（X轴），单位 度<br/>
      roll：人脸旋转角度，翻滚角（Z轴），单位 度</td>
   </tr>
   <tr>
      <td>isValidPosture</td>
      <td>bool</td>
      <td>true</td>
      <td>人脸角度是否在合理的阈值内</td>
   </tr>
   <tr>
      <td>blurScore</td>
      <td>float</td>
      <td>0.03</td>
      <td>人脸模糊度，值越低越模糊，越高越清晰</td>
   </tr>
</table>

### 2、返回示例 

```JSON
{
    "code": "10000",
    "charge": true,
    "remain": 996,
    "remainTimes": 996,
    "remainSeconds": -1,
    "msg": "查询成功,扣费",
    "result": {
        "code": 0,
        "faceItemsNir": [
            {
                "blurScore": "0.21",
                "boundingBox": {
                    "height": "133.65",
                    "left": "365.02",
                    "top": "20.81",
                    "width": "102.35"
                },
                "isValidPosture": true,
                "posture": {
                    "pitch": "-4.59",
                    "roll": "-9.92",
                    "yaw": "-3.87"
                }
            }
        ],
        "faceItemsVisual": [
            {
                "blurScore": "0.21",
                "boundingBox": {
                    "height": "133.65",
                    "left": "365.02",
                    "top": "20.81",
                    "width": "102.35"
                },
                "isValidPosture": true,
                "posture": {
                    "pitch": "-4.59",
                    "roll": "-9.92",
                    "yaw": "-3.87"
                }
            }
        ],
        "msg": "Accept",
        "processTimeInMs": 73,
        "score": "1.00",
        "timestamp": 1585189871930
    }
}
```
