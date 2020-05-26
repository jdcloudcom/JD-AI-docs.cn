### 商品图片删除

#### 1. 描述

商品图片删除接口，删除用户指定的某商品库中某商品的图片，支持批量删除。


#### 2. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/product_image_del_image
```

#### 3. 请求方式：

https `post` aiapi.jdcloud.com/jdai/product_image_del_image

#### 4. 请求参数

##### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）query请求参数

##### （3）body请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
collection_name | string | 是 | 服饰商品库 | 要删除的商品库名称
image_id_list | array | 是 | [...] |要删除的图片列表

image_id_list参数说明

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
product_id | string | 是 | 65337027695 | 商品唯一标识，即SKU
image_id | string | 是 | 1002039492343.jpg | 图片的唯一标识

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

result参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code| int | 0 | 参照概述-业务错误码
message | string | "SUCCESS" | 参照概述-业务错误信息
successful_list | array | [...] | 删除成功的图片列表
failed_list | array | [...] | 删除失败的图片列表

succeeded_list参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
product_id | string | 65337027695 | 删除成功的图片所属商品的ID（SKU）
image_id | string | 1002039492343.jpg | 删除成功的图片的ID

failed_list 参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
product_id | string | 65337027695 | 删除失败的图片所属商品的ID（SKU）
image_id | string | 1002039492343.jpg | 删除失败的图片的ID
message | string | "NO_AVAILABLE_FEATURE" | 删除失败的原因

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
      "message": "SUCCESS",
      "successful_list": [
        {
          "image_id": "a0906237d2cd30ad.jpg",
          "product_id": "102340326"
        }
      ]
  }
}
```