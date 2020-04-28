# 词义相似度

## 一、接口描述

### 1. 功能描述
> 根据输入的两个词语，计算两个词语的相似度，相似度越大的两个词在词义上越相似

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/similar
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/similar

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/json | 标准编码格式
x-ai-request-id | string | 否 | 2f21e3de77ba4b4ab03cadb823ad145c | 格式：UUID.randomUUID().toStri ng().replace("-","")

#### （2）query请求参数

#### （3）body请求参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>word1</td>
      <td>string</td>
      <td>是</td>
      <td>快递1</td>
      <td>词1</td>
   </tr>
  <tr>
     <td>word2</td>
     <td>string</td>
     <td>是</td>
     <td>快递2</td>
     <td>词2</td>
  </tr>
</table>

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

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>score</td>
      <td>float</td>
      <td>0.45666688</td>
      <td>相似度数值</td>
   </tr>
   <tr>
      <td>words</td>
      <td>object</td>
      <td>{"word1":"电脑","word2":"平板"}</td>
      <td>相似度词组</td>
   </tr>
</table>

### 2、返回示例

```JSON
{
    "score":0.45666688,
    "words":{
        "word1":"电脑",
        "word2":"平板"
    }
}
```

### 3、业务错误码
<table>
   <tr>
      <th>业务错误码（status）</th>
      <th>message </th>
      <th>说明 </th>
   </tr>
   <tr>
      <td>1000</td>
      <td>"Request OK"</td>
      <td>查询成功</td>
   </tr>
   <tr>
      <td>1001</td>
      <td>"Request Coding Error"</td>
      <td>输入参数编码错误</td>
   </tr>
   <tr>
      <td>1002</td>
      <td>"Request OverLength Error"</td>
      <td>输入参数编码错误</td>
   </tr>
   <tr>
      <td>1003</td>
      <td>"Request Empty Error"</td>
      <td>输入参数长度过长</td>
   </tr>
   <tr>
      <td>20001</td>
      <td>"Words Not Found Error"</td>
      <td>查找不到词语</td>
   </tr>
   <tr>
      <td>30001</td>
      <td>"Unknown Error"</td>
      <td>未知错误</td>
   </tr>
</table>