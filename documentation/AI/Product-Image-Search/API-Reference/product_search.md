### 商品图片搜索

#### 1. 描述

商品图片搜索接口，根据请求的图片，从已入库的图片中召回满足条件的图片。


#### 2. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/product_image_search
```

#### 3. 请求方式：

https `post` aiapi.jdcloud.com/jdai/product_image_search

#### 4. 请求参数

##### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）query请求参数

##### （3）body请求参数

业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
image_content | string | 是 | 【略】 | 要搜索的图片内容，URL或Base64编码
collection_name | string | 是 | "服装商品库" | 指定搜索的商品库名称
category | string | 否 | "服装" | 搜索商品的类别【"服装"、"鞋靴"、"其他"】之一
topk | int | 否 | 10 | 召回的图片数量，如不指定，默认50，最多200

#### 5. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

#### 6. 返回说明
##### 1、返回参数

###### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


###### （2）业务返回参数
服务器返回的识别结果采用 JSON 格式：

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code| int | 0 | 参照概述-业务错误码
message | string | "SUCCESS" | 参照概述-业务错误信息
rectangle | object | {...} | 搜索商品图中商品的检测框坐标
images | array | [...] | 从图片库中召回的相似图片信息列表

rectangle 参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
bottom | float | 763.3587646484375 | 检测框最下边的纵坐标
top | float | 40.80238342285156 | 检测框最上边的纵坐标
left | float | 34.845638275146484 | 检测框最左边的横坐标
right | float | 765.8860473632812 | 检测框最右边的横坐标

images 参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
product_id | string | "65337027695" | 召回的图片所属商品的ID
product_name | string | "女士风衣" | 召回的图片所属商品的名称
image_id | string | "1002039492343.jpg" | 召回的图片的唯一标识
similarity | float | 0.98323532 | 召回的图片和搜索图片的相似度
image_info | string | 【略】| 召回的图片的额外描述信息

##### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": false,
  "remainTimes": 4998,
  "remainSeconds": -1,
  "msg": "查询成功",
  "result": {
      "code": 0,
      "images": [
        {
          "image_id": "a0906237d2cd30ad.jpg",
          "info": "",
          "product_id": "102340326",
          "product_name": "笔记本电脑",
          "similarity": 0.49002131769384594
        },
        {
          "image_id": "35e94ca3e9d9fdf9.jpg",
          "info": "",
          "product_id": "102340325",
          "product_name": "电视",
          "similarity": 0.22615687617595456
        }
      ],
      "message": "SUCCESS",
      "rectangle": [
        {
          "bottom": 763.3587646484375,
          "left": 34.845638275146484,
          "right": 765.8860473632812,
          "top": 40.80238342285156
        }
      ]
  }
}
```