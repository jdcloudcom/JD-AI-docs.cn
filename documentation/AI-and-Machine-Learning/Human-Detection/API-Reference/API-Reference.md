# 人体检测

## 一、接口描述 

### 1.功能描述
人体检测API主要用于对传入的图片中所有人体的位置进行检测，返回其坐标值以及置信度。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3.图片要求

> 1. 图片格式：jpg、jpeg、png
> 2. 图片像素尺寸：最小 256\*256 像素，最大 4096\*4096 像素
> 3. 图片文件大小：小于2M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/human_detect
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/human_detect

### 3. 请求参数  

#### （1）header请求参数
业务请求参数

名称  | 类型  | 必填  | 示例值  | 描述
------|-----|-----|-----|-----
Content-Type | String | 是 | application/octet-stream| 表示在发送到服务器之前，所有字符都会进行编码。
Authorization  | string  | 是  | JDCLOUD2-HMAC-SHA256Credential=access...  | 签名

#### （2）body请求参数
业务请求参数

名称  | 类型  | 必填  | 示例值  | 描述
------|-----|-----|-----|-----
无  | binary  | 是  | 采用二进制方式读取图片  | 图片内容，传入图片


### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)
 
## 返回说明

### 1、返回参数
#### （1）公共返回参数

名称  | 类型  | 示例值  | 描述
------|-----|-----|-----
code  | string  | 1000  | 参见[错误码](Error-Code.md)-系统级错误码
charge  | boolean  | false 或 true  | false：不扣费， true：扣费
remain  | long  | 1305  | 按天计算剩余调用次数
msg  | string  | 查询成功  | 参见[错误码](Error-Code.md)-系统级错误码
result  | object  | {...}  | 查询结果


#### （2）业务返回参数

名称  | 类型  | 示例值  | 描述
------|-----|-----|-----
status  | int  | 0  | 返回结果，0表示成功；非0为对应错误号，参见[错误码](Error-Code.md)-业务级错误码
message  | string  | ok  | 错误信息，参见[错误码](Error-Code.md)-业务级错误码
used_time  | int  | 198  | 整个请求花费的时间，单位为毫秒
request_id  | string  | 1544940159.6349967  | 便于双方定位问题
humanDetectionResult  | array  | [[x1,y1,x2,y2,score],[x1,y1,x2,y2,score],...]  | x1,y1,x2,y2,score分别表示预测出的人体矩形框的左上角坐标，右下角坐标，以及置信度。返归的矩形框按照置信度高低排序，当未检测到人体时，返回空array[]。 

### 2、返回示例

```Json
{
    "code": 10000, 
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": 
    {
    	"status":0,
    	"request_id": "1544940159.6349967",
        "message":"ok",
        "used_time":95,
        "humanDetectionResult":
        [
            [319, 170, 395, 302, 1.0],
            [265, 173, 324, 295, 1.0],
            [265, 127, 314, 261, 0.96]
        ]    
    }
}
```
