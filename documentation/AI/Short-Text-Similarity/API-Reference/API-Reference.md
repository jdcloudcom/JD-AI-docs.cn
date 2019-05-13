# 短文本相似度

## 一、接口描述 
### 1. 功能描述  
短文本相似度API提供不同短文本之间相似度的计算，输出的相似度是一个介于0到1之间的实数值，越大则相似度越高。这个相似度值可以直接用于结果排序，也可以作为一维基础特征作用于更复杂的系统。

### 2. 接口使用：

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/similarity
```
### 2. 请求方式：  
https `get/post` aiapi.jdcloud.com/jdai/similarity

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | string | 是 | application/json | 表示请求JSON格式的文本信息
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
text1 | string | 是 | 克林顿访问中国 | 输入文本1
text2 | string | 是 | 尼克松访华 | 输入文本2

### 4、请求代码示例

建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数
*status、message、request_id根据网关定义如下，如不一致请同步给产品经理*

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status | int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | OK | 参见[错误码](Error-Code.md)-业务级错误码
request_id | string | 5893465d31284468a8014de6ee430f8e | 便于双方定位问题
similarity | object | {"score":0.19182715292135427,<br/>"text1":"克林顿访问中国",<br/>"text2":"尼克松访华"} | 相似度结果，，详情下面similarity字段说明


#### similarity字段说明

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
text1 | string | 克林顿访问中国 | 输入文本1
text2 | int | 尼克松访华 | 输入文本2
score | double | 0.19182715292135427 | 相似度 0~1，分数越高表示两个文本越相似。


### 2、返回示例  
*此处内容为通过网关后返回的结果，包含公共返回参数*   

```
{
"code": "10000",
    "charge": false,
    "remain": 0,
    "msg": "查询成功",
    "result": {
         "status": 0,
         "request_id": "8f47d951-34fe-4fac-b96c-d60d0a9bd719",
         "message": "ok",
         "similarity": {
              "score": 0.19182715292135427,
              "text1": "克林顿访问中国",
              "text2": "尼克松访华"
         }
    }
}    
```


	


