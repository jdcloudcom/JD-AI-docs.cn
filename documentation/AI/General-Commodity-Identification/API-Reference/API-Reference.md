# 通用商品识别

## 一、接口描述

### 1. 功能描述
> 通用商品识别接口识别图片中主体显著物体，进行识别，返回商品的细粒度类别信息。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明：
  通用商品识别是人工智能计算机视觉技术的通用能力，京图搜产品依靠2.7亿商品以及近10亿商品图的数据积累，实现覆盖多品类的面向零售场景的商品识别能力。

### 4. 接口数据要求：
> 1. 图片格式：Base64
> 2. 图片大小：小于 3.75M
> 3. 图像类型：jpg/jpeg/png

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/image_recognition_product
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/image_recognition_product

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | text/plain | 标准编码格式
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）query请求参数

#### （3）body请求参数

业务请求参数

```
imgBase64=xxx(图像Base64编码值，去掉图片头"data:image/png;base64,"，imageBase64=iVBORw0K...（由于过长，不给出示例）)
```
其中，各参数定义如下

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imgBase64 | String | 是 | 图像Base64编码值，去掉图片头"data:image/png;base64,"，<br/>imgBase64=iVBORw0K...（由于过长，不给出示例） | 图片base64编码
multi_box | bool | 否 | multi_box=true | 是否返回多主体

> 注意：multi_box预留参数，当前不支持

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

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status| int | 0 | 参照四、错误码-业务错误码
message | string | "Interface Succeed!" | 参照四、错误码-业务错误信息
item|  list| [...]|  商品信息列表

item参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
cid_list | list | [...] | 商品1到4级类目信息
rectangle | obj | {...} | 商品坐标信息

cid_list参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
root | string | 玩具乐器 | 细类目名称
score|float|0.9708835|类目置信度得分

rectangle参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
bottom | float | 538.3639892578125 | 右下角y值
confidence|float|0.6000407338142395|物体框选置信度
left|float|66.85603637695313|左上角x值
right|float|852.2189208984374|右下角x值
top|float|111.47796020507812|左上角y值

### 2、返回示例

```JSON
{
    "code": "10000",
        "charge": false,
        "remain": 0,
        "remainTimes": -1,
        "remainSeconds": -1,
        "msg": "查询成功",
        "result": {
          "items": [
            {
              "cid_list": [
                {
                  "root": "玩具乐器",
                  "score": 0.9708835
                },
                {
                  "root": "母婴",
                  "score": 0.89061433
                },
                {
                  "root": "童车童床",
                  "score": 0.941696
                },
                {
                  "root": "电动车",
                  "score": 0.65561
                }
              ],
              "rectangle": {
                "bottom": 538.3639892578125,
                "confidence": 0.6000407338142395,
                "left": 66.85603637695313,
                "right": 852.2189208984374,
                "top": 111.47796020507812
              }
            }
          ],
          "message": "Inference Succeed!",
          "status": "0"
        }
    }
}
```

### 3、业务错误码
业务错误码（status）|message|说明
------|------|------
10002|"base64 data is too large!"|图像过大
10004|"base64 data error!"|图像格式错误
10005|"input error! not supported!"|不支持的图像类型