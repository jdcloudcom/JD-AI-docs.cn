# 智能写作

## 一、接口描述

### 1. 功能描述
> 商品营销卖点智能挖掘与营销内容智能写作

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/intelligent_creation
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/intelligent_creation

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/json | 标准编码格式

#### （2）query请求参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>sku</td>
      <td>string</td>
      <td>是</td>
      <td>100006079301</td>
      <td>京东商品sku编码</td>
   </tr>
</table>

#### （3）body请求参数

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
服务器返回的识别结果采用 JSON 格式：

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
    <tr>
      <td>code</td>
      <td>int</td>
      <td>200</td>
      <td>返回码</td>
   </tr>
   <tr>
      <td>msg</td>
      <td>string</td>
      <td>空</td>
      <td>返回码解释，成功为空</td>
   </tr>
      <tr>
      <td>data</td>
      <td>object</td>
      <td>{...}</td>
      <td>业务内容</td>
   </tr>
   <tr>
      <td>title</td>
      <td>string</td>
      <td>兰蔻 雾面哑光 化妆品套装</td>
      <td>短标题</td>
   </tr>
   <tr>
      <td>content</td>
      <td>string</td>
      <td>兰蔻的这款唇膏，蕴含丰富的滋养成分，可以有效的为肌肤补充所需的营养，改善干燥、粗糙的肤质。质地温和的特点，不会刺激皮肤</td>
      <td>商品营销短文</td>
   </tr>
      <tr>
      <td>htmlContent</td>
      <td>string</td>
      <td>兰蔻的这款唇膏，蕴含丰富的<strong>滋养</strong>成分，可以有效的为肌肤补充所需的营养，<strong>改善干燥</strong>、粗糙的肤质。<strong>质地温和</strong>的特点，不会刺激皮肤。</td>
      <td>商品卖点，<strong>滋养</strong>标示“滋养”卖点
</td>
   <tr>
      <td>version</td>
      <td>string</td>
      <td>1.0.2.O</td>
      <td>模型标记</td>
   </tr>
   </tr>
</table>

### 2、返回示例

```JSON
{
    "msg": "",
    "code": 200,
    "data": {
        "title": "兰蔻 胡萝卜色 化妆品套装",
        "content": "兰蔻的这款唇膏，蕴含丰富的滋养成分，能够有效的改善干燥、粗糙的肤质，同时还能促进后续保养品的吸收。质地温和的特点，不会刺激皮肤。",
        "htmlContent": "兰蔻的这款唇膏，蕴含丰富的<strong>滋养</strong>成分，能够有效的<strong>改善干燥</strong>、粗糙的肤质，同时还能促进后续保养品的吸收。<strong>质地温和</strong>的特点，不会刺激皮肤。"
    },
    "version": "1.0.2.O"
}
```

### 3、业务错误码
<table>
   <tr>
      <th>业务错误码（status）</th>
      <th>说明 </th>
   </tr>
   <tr>
      <td>500</td>
      <td>没有相关知识</td>
   </tr>
</table>
