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
      <td>text1</td>
      <td>string</td>
      <td>是</td>
      <td>克林顿访问中国</td>
      <td>输入文本1</td>
   </tr>
   <tr>
      <td>text2</td>
      <td>string</td>
      <td>是</td>
      <td>尼克松访华</td>
      <td>输入文本2</td>
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
*status、message、request_id根据网关定义如下，如不一致请同步给产品经理*

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
      <td>OK</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
      <tr>
      <td>request_id</td>
      <td>string</td>
      <td>5893465d31284468a8014de6ee430f8e</td>
      <td>便于双方定位问题</td>
   </tr>
   <tr>
      <td>similarity</td>
      <td>object</td>
      <td>{"score":0.19182715292135427,"text1":"克林顿访问中国","text2":"尼克松访华"}</td>
      <td>相似度结果，，详情下面similarity字段说明</td>
   </tr>
</table>

#### similarity字段说明
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>text1</td>
      <td>string</td>
      <td>克林顿访问中国</td>
      <td>输入文本1</td>
   </tr>
   <tr>
      <td>text2</td>
      <td>int</td>
      <td>尼克松访华</td>
      <td>输入文本2</td>
   </tr>
   <tr>
      <td>score</td>
      <td>double</td>
      <td>0.19182715292135427</td>
      <td>相似度 0~1，分数越高表示两个文本越相似。</td>
   </tr>
</table>

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


	


