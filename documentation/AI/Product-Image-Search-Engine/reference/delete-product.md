### 商品删除

#### 1. 描述

商品删除接口，删除指定商品库中的商品，连同该商品的图片一起删除。支持批量商品删除。<br>
图片及接口的通用信息说明，详见 [服务概述](api-reference.md)


#### 2. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/product_image_del_product
```

#### 3. 请求方式：

https `post` aiapi.jdcloud.com/jdai/product_image_del_product

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
collection_name | string | 是 | 服饰商品库 | 商品库名称
product_id_list | array | 是 | ["104631367"] | 要删除的商品的SKU列表

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
successful_list | array | ["104631367"] | 删除成功的商品SKU列表
failed_list | array | [...] | 删除失败的商品信息列表

failed_list参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
product_id | string | "104631367" | 删除失败的商品SKU
message | string | "NOT_EXISTING_PRODUCT" | 删除失败的原因


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
      "failed_list": [],
      "message": "SUCCESS",
      "successful_list": [
        "102340325"
      ]
  }
}
```