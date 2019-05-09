# 文本分类

## 一、接口描述 
### 1. 功能描述  
  识别用户话术的领域信息，当前版本在13个领域上进行分类：歌曲、广播、故事、百科、天气、时间、新闻、生活查询、岀行、股票、购物、音箱指令、家居指令、闲聊、翻译、计算机、闹钟。
<table>
   <tr>
      <th>types</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
   </tr>
   <tr>
      <td>domain name</td>
      <td>other</td>
      <td>calcu</td>
      <td>chat</td>
      <td>info</td>
      <td>instruct</td>
      <td>local</td>
      <td>news</td>
   </tr>
</table>

<table>
   <tr>
      <th>types</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
   </tr>
   <tr>
      <td>domain name</td>
      <td>radio</td>
      <td>reject</td>
      <td>song</td>
      <td>story</td>
      <td>weather</td>
      <td>shopping</td>
   </tr>
</table>

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)。


## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/textClassification
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/textClassification

### 3. 请求参数

#### （1）header请求参数
业务请求参数
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>string</td>
      <td>是</td>
      <td>application/json</td>
      <td>表示请求JSON格式的文本信息</td>
   </tr>
   <tr>
      <td>Authorization</td>
      <td>string</td>
      <td>是</td>
      <td>JDCLOUD2-HMAC-SHA256Credential=access...</td>
      <td>签名</td>
   </tr>
</table>

#### （2）body请求参数
业务请求参数
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>必填</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>text</td>
      <td>string</td>
      <td>是</td>
      <td>克林顿访问中国</td>
      <td>输入文本</td>
   </tr>
</table>

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)


## 三、返回说明
### 1、返回参数
#### （1）公共返回参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>code</td>
      <td>string</td>
      <td>1000</td>
      <td>参见下方错误码-系统级错误码</td>
   </tr>
      <tr>
      <td>charge</td>
      <td>boolean</td>
      <td>false 或 true</td>
      <td>false：不扣费， true：扣费</td>
   </tr>
      <tr>
      <td>remain</td>
      <td>long</td>
      <td>1305</td>
      <td>按天计算剩余调用次数</td>
   </tr>
      </tr>
      <tr>
      <td>msg</td>
      <td>string</td>
      <td>查询成功</td>
      <td>参见下方错误码-系统级错误码数</td>
   </tr>
      </tr>
      <tr>
      <td>result</td>
      <td>object</td>
      <td>{...}</td>
      <td>查询结果</td>
   </tr>
</table>

#### （2）业务返回参数

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>status</td>
      <td>int</td>
      <td>0</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
      <tr>
      <td>message</td>
      <td>string</td>
      <td>ok</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
      <tr>
      <td>request_id</td>
      <td>string</td>
      <td>5893465d31284468a8014de6ee430f8e</td>
      <td>便于双方定位问题</td>
   </tr>
   <tr>
      <td>types</td>
      <td>list</td>
      <td> [{"type": 3, "probability": 0.727774441242218, "domainName": "info"},,...] </td>
      <td>文本分类结果，详情下面types字段说明</td>
   </tr>
</table>

#### types字段说明
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>type</td>
      <td>int</td>
      <td>3</td>
      <td>分类序号</td>
   </tr>
   <tr>
      <td>probability</td>
      <td>double</td>
      <td>0.727774441242218</td>
      <td>分类概率</td>
   </tr>
   <tr>
      <td>domainName</td>
      <td>string</td>
      <td>info</td>
      <td>分类名称</td>
   </tr>
</table>


### 2、返回示例


```
{
    "code": "10000",
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": {
                "status": 0,
                "request_id": xxx,
                "message": "ok",
                "types": [
                  {
                    "type": 3,
                    "probability": 0.727774441242218,
                    "domainName": "info"
                  },
                  {
                    "type": 8,
                    "probability": 0.2294873297214508,
                    "domainName": "reject"
                  },
                  {
                    "type": 9,
                    "probability": 0.042706381529569626,
                    "domainName": "song"
                  }
                ]
              }
}
```
