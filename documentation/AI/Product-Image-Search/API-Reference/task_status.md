### 入库状态查询

#### 1. 描述

入库状态查询接口，根据商品图片入库返回的异步任务ID，查询图片入库状态，仅支持单个任务查询。


#### 2. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/product_image_status
```

#### 3. 请求方式：

https `post` aiapi.jdcloud.com/jdai/product_image_status

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
task_id | string | 是 | "92374205376234/food/1573113266.7619262" | 查询的入库任务ID

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
task_status | string | "FINISHED" | 任务状态，有"PROCESSING", "FINISHED"两种。其中FINISHED仅表示任务处理完成，各图片是否入库成功需要查看succeeded_list和failed_list
succeeded_list | array | [...] | 返回入库成功的图片名列表，**仅当status_code为0时存在**
failed_list | array | [...] | 返回入库失败的图片列表，**仅当status_code为0时存在**

succeeded_list 参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
product_id | string | 65337027695 | 入库成功的图片所属商品的ID（SKU）
image_id | string | 1002039492343.jpg | 入库成功的图片的ID

failed_list 参数说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
product_id | string | 65337027695 | 入库失败的图片所属商品的ID（SKU）
image_id | string | 1002039492343.jpg | 入库失败的图片的ID
message | string | "NO_AVAILABLE_FEATURE" | 入库失败的原因

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
      "pending_list": [],
      "succeeded_list": [
        "1001/XX小店|102340325|35e94ca3e9d9fdf9.jpg",
        "1001/XX小店|102340326|a0906237d2cd30ad.jpg"
      ],
      "task_status": "FINISHED"
  }
}
```