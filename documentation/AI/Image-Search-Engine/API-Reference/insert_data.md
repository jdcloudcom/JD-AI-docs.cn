### 图片入库请求

#### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/index
```

#### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/index

#### 3. 请求参数

#####（1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）query请求参数

##### （3）body请求参数
名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
collection_name | string | 是 | "food" | 库名，每个用户最多创建3个图片库
docs| array| 是 | [...] | 入库图片列表

docs参数信息

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
image_name | string | 是 | "Milk_salt_soda_v1" | 图片名，作为图片的唯一标识<br>，由用户自定义，用于后续查<br>询等操作，最大长度为50字<br>符，支持utf8编码；
image_content | string | 是 | "http://img10.360buyimg.com/<br>da/jfs/xxxxxxx.jpg" | 图片url或者base64编码(去掉图片头<br>"data:image/png;base64,")，<br>url目前仅支持存储在JSF服务器<br>的图片链接；若有大规模图片<br>入库需求，请联系我们。
info | string | 否 | "{\"Ingredients\":\"wheat flour, milkfat, <br>edible salt\", \"price\":\"10.0\"}" | 图片的备注信息，最大长度<br>为300字符，如有提供，搜索时<br>将一并返回

#### 4. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

### 返回说明
#### 1、返回参数

##### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


##### （2）业务返回参数
服务器返回的识别结果采用 JSON 格式：

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status_code| int | 0 | 参照概述-业务错误码
message | string | "SUCCESS" | 参照概述-业务错误信息
task_id| string | "92374205376234/food/1573113266.7619262" | 本次请求的任务id，可用于查询任务状态(包含后续流程中 待处理/处理成功/处理失败 的图片列表)
failed_list | array | [...] | 传入的docs中即时检查失败的doc列表(url或base64无效、info过长、图片名已存在库中等情况)，**仅当status_code为0时存在**

failed_list 参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
image_name | string | "DUPLICATE_EGG" | 图片名
message | string | "REPEAT_IMAGE_NAME_IN_DB" | 即时检查的失败信息

#### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": false,
  "remainTimes": 4998,
  "remainSeconds": -1,
  "msg": "查询成功",
  "result": {
    "status_code": 0,
    "message": "SUCCESS",
    "task_id": "92374205376234/food/1573113266.7619262",
    "failed_list": [
      {
        "image_name": "DUPLICATE_EGG",
        "message": "REPEAT_IMAGE_NAME_IN_DB"
      },
      ……
    ]
  }
}
```