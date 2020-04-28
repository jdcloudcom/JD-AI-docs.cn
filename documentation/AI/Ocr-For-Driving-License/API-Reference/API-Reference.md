# 驾驶证识别

## 一、接口描述

### 1. 功能描述
> 驾驶证识别，可对输入的图片自动识别驾驶证信息，兼顾驾驶证首页和副页，提取驾驶人员的身份信息，输出关键字段。

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 图片要求

> 1. 图片格式：jpg/jpeg、png
> 1. 图片大小：小于5M

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/ocr_driver_license
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/ocr_driver_license

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/octet-stream | 标准编码格式

#### （2）query请求参数

#### （3）body请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
无 | binary | 是 | 无 | 图片内容，传入图片

### 4. 请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


## 三、返回说明
### 1、返回参数

#### （1）公共返回参数

名称 | 类型 | 示例值 | 描述
------|------|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果


#### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code|	int|	0|	参照四、错误码-业务错误码
message|	string|	success|	状态码描述
request_id|	string|	cb4f53b8c60e9589445cc4cd895cf5b6|	为方便定位问题的32位uuid
resultData|	object|	{...}|	返回识别结果

resultData参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
id | String | 530425198801020925 | 证件号
name |String | 李敏 | 姓名
sex | String | 女 |性别
address | String | 云南省玉溪市易门县铜厂彝族乡街坡村61号 |地址
birthday | String | 1988-01-02 |生日
class | String | C1 | 准驾车型
country | String |中国 |国籍
file_id | String | 110008768680|档案编号
issue_date | String | 2008-10-09 |初次领证日期
valid_for | String | 6年 |有效期
valid_from | String | 2008-10-09 |有效起始日期
record | String | 实习期至2020-10-01 | 检验记录

### 2、返回示例

```JSON
{
	"code": 0,
	"message": "success",
	"request_id": "439e5968-7587-11ea-af0e-fa163ea0a74a",
	"resultData": {
		"address": "云南省玉溪市易门县铜厂彝族乡街坡村61号",
		"birthday": "1988-01-02",
		"class": "C1",
		"country": "中国",
		"file_id": "110008768680",
		"id": "530425198801020925",
		"issue_date": "2008-10-09",
		"name": "李敏",
		"record": "实习期至2020-10-01",
		"sex": "女",
		"valid_for": "6年",
		"valid_from": "2008-10-09"
	}
}
```

### 3、业务错误码
业务错误码（code）|message|说明
------|------|------
12001|"image does not exist"|图像不存在
12002|"image format error"|图像格式错误
12003|"image size error, 5M Limit"|图像大小错误
13002|"time out"|超时
13004|"no content recognition"|无内容识别
13005|"other error"|其他错误