# 创建人脸分组

## 一、接口描述 

### 1.功能描述

创建一个人脸分组，用于存储人脸。一个分组能够存储100000张人脸。一个用户的分组最多不能超过5个。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。


## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/faceGroupCreate
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/faceGroupCreate

### 3. 请求参数  
 
#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述 
------|-----|-----|-----|-----
Authorization  | string  | 是  | JDCLOUD2-HMAC-SHA256Credential=access...  | 签名


#### （2）query请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述 
------|-----|-----|-----|-----
groupName  | string  | 是  | test  | 分组名称, 不支持中文以及特殊字符
groupInfo  | string  | 否  | test test  | 分组描述，支持中文和特殊字符


### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)
 
## 返回说明

### 1、返回参数

#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|-----|-----|----- 
code  | string  | 1000  | 参见[错误码](Error-Code.md)-系统级错误码
charge  | boolean  | false 或 true  | false：不扣费， true：扣费
remain  | long  | 1305  | 按天计算剩余调用次数
msg  | string  | 查询成功  | 参见[错误码](Error-Code.md)-系统级错误码
result  | object  | {...}  | 查询结果


#### （2）业务返回参数

名称 | 类型 | 示例值 | 描述 
------|-----|-----|-----
status  | int  | 0  | 返回结果，0表示成功；非0为对应错误号，参见[错误码](Error-Code.md)-业务级错误码
message  | string  | Success  | 若status为0，返回分组id，否则返回错误信息，参见[错误码](Error-Code.md)-业务级错误码


### 2、返回示例

```Json
{
    "status": 0, 
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": 
    {
    	    "requestid": "6979e9bd79b944b49e0d6e74079d5098",
            "message": "8b94af03-67d7-47ec-ae56-bc5d50333076",
            "status": 0
    }
}
```
