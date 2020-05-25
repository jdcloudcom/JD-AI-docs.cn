### 商品图入库

#### 1. 描述

商品图入库接口，支持用户单个图片入库和批量图片入库操作。对于单个图片入库，用户可提供URL和Base64编码格式图片作为参数；
对于批量图片入库，用户需提供URL格式图片作为参数。商品图片入库请求提交后，即创建一个异步入库任务，并返回任务ID。


#### 2. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/product_image_add
```

#### 3. 请求方式：

https `post` aiapi.jdcloud.com/jdai/product_image_add

#### 4. 数据要求

> * 图片格式：图片URL或Base64编码，URL仅支持JFS格式。
> * 图片像素：最小 201 \* 201，最大 4096 \* 4096
> * 图片大小：小于 3.75M
> * 图片类型：jpg, jpeg, png
> * 批量入库图片URL数量最多为200。

#### 5. 请求参数

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
collection_name | string | 是 | 服饰商品库 | 商品库名称，如果不存在，会自动创建，每个用户最多拥有1个商品库
image_list | string | 是 | [...] | 图片列表

image_list参数说明

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
product_id | string | 是 | 65337027695 | 商品唯一标识，即SKU
image_content | string | 是 | 【略】 | 图片内容，URL或Base64编码
image_id | string | 是 | 1002039492343.jpg | 图片的唯一标识，可以为图片名称，不可重复
image_info | string | 否 | 【略】| 用于图片描述，最多支持256个字符输入


#### 6. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

#### 7. 返回说明
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
task_id| string | "92374205376234/food/1573113266.7619262" | 本次请求的任务id，可用于查询任务状态(包含后续流程中 待处理/处理成功/处理失败 的图片列表)
failed_list | array | [...] | 返回传入的docs中即时检查失败的doc列表(url或base64无效、info过长、图片名已存在库中等情况)，**仅当status_code为0时存在**

failed_list 参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
image_id | string | "DUPLICATE_IMAGE" | 图片名
message | string | "REPEAT_IMAGE_NAME_IN_DB" | 即时检查的失败信息

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
      "task_id": "1001/XX小店/1581417512.274598"
  }
}
```