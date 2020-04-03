### 图片搜索请求

#### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/index_search
```

#### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/index_search

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
collection_name | string | 是 | "food" | 库名
query_content | string | 是 | 图像Base64编码值，去掉图片头"data:image/png;base64,"，query_content=iVBORw0K...（由于过长，不给出示例） | 图片base64编码
top_k | int | 否 | 50 | 召回数量，默认50，最大200

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
message | string | "Interface" | 参照概述-业务错误信息
search_result | array | [...] | 搜索结果

search_result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
image_name | string | "Milk_salt_soda_v1" | 召回图片所属集合id,入库时提供
similarity | double | 0.92323356 | 召回图片和请求图的相似度；当为1时，即两张图为完全一样的图片；
info | string | "{\"Ingredients\":\"wheat flour, milkfat, edible salt\", \"price\":\"10.0\"}" | 召回图片所带json信息，仅在入库时附带了此信息时返回

#### 2、返回示例

```JSON
{
  "code": "10000",
  "charge": false,
  "remainTimes": 4998,
  "remainSeconds": -1,
  "msg": "查询成功",
  "result": {
    "status_code":0,
    "message":"SUCCESS",
    "search_result":[
      {
        "image_name":"Milk_salt_soda_v1",
        "similarity":0.92323356,
        "info ":'{"Ingredients":"wheat flour, milkfat, edible salt", "price":"10.0"}'
      },
      ……
    ]
  }
}
```