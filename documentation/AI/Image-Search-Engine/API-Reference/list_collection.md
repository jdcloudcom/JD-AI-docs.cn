### 库列表查询请求
库列表查询请求接口用于查询用户目前创建的哪些图片库及对应的库中已入库的图片数量<br>
图片及接口的通用说明详见 [服务概述](API-Reference.md)

#### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/collection_list
```

#### 2. 请求方式：

https `get` aiapi.jdcloud.com/jdai/collection_list

#### 3. 请求参数

#####（1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Content-Type | String | 是 | application/json| 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

##### （2）query请求参数

##### （3）body请求参数
无

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
collection_list | array | [...] | 用户拥有的库的信息列表

collection_list 参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
collection_name | string | "food" | 库名    
indexed\_image_count | string | 100 | 已入库图片数

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
    "collection_list": [
      {
        "collection_name":"bags",
        "indexed_image_count":30
      }
    ]
  }
}
```