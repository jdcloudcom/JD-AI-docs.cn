# 车辆检测

## 一、接口描述

### 1. 功能描述
> 车辆检测API能够准确地检测出图片中车辆的位置，返回其坐标与置信度。

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 图片要求

> 1. 图片格式：jpg、jpeg、jfif、png
> 2. 图片像素尺寸：最小 256\*256 像素，最大 4096\*4096 像素
> 3. 图片文件大小：小于2M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/vehicle_detection
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/vehicle_detection

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/octet-stream | 标准编码格式

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
      <td>是</td>
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
      <td>返回结果，0表示成功，非0为对应错误号</td>
   </tr>
   <tr>
      <td>message</td>
      <td>string</td>
      <td>ok</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>used_time</td>
      <td>int</td>
      <td>53</td>
      <td>整个请求花费的时间，单位为毫秒</td>
   </tr>
   <tr>
      <td>request_id</td>
      <td>string</td>
      <td>1544940159.6349967</td>
      <td>便于双方定位问题</td>
   </tr>
   <tr>
      <td>vehicleDetectionResult</td>
      <td>array</td>
      <td>[[x1,y1,x2,y2,score],[x1,y1,x2,y2,score],...]</td>
      <td>x1,y1,x2,y2,score分别表示预测出的车辆矩形框的左上角坐标，右下角坐标，以及置信度。返归的矩形框按照置信度高低排序，当未检测到车辆时，返回空array[]。</td>
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
        "used_time":53,
        "vehicleDetectionResult":
        [
            [319, 170, 395, 302, 1.0],
            [265, 173, 324, 295, 1.0],
            [265, 127, 314, 261, 0.96]
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
      <td>12002</td>
      <td>not enough param</td>
      <td>参数缺失（未传入任何图片）</td>
   </tr>
   <tr>
      <td>12003</td>
      <td>image type error</td>
      <td>解析参数错误,图片格式不支持</td>
   </tr>
   <tr>
      <td>12004</td>
      <td>image size exceeds 2M </td>
      <td>图片大小超过限制，图像超过2M</td>
   </tr>
      <tr>
      <td>12004</td>
      <td>image size must be between 256X256 and 4096X4096 </td>
      <td>图片大小超过限制，图片尺寸不在支持范围内，与上方情况共用一个错误码</td>
   </tr>
</table>