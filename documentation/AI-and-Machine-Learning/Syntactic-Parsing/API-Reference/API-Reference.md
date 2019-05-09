# 句法分析

## 一、接口描述 
### 1. 功能描述
提供文本中词与词之间的依存关系和句法结构信息（如：主谓宾、定状补），帮助机器实现对用户意图的准确理解。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](https://neuhub.jd.com/ai/api/nlp/systax)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](https://aidoc.jd.com/user/auth.html)规则进行相应开发，整体流程详见   [接入流程](https://aidoc.jd.com/user/flow.html)  。


## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/parser
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/parser

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
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](未发布)


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
      <td>dependencyRelation</td>
      <td>string</td>
      <td>nsubj</td>
      <td>依存关系标识</td>
   </tr>
   <tr>
      <td>parent</td>
      <td>string</td>
      <td>2</td>
      <td>父节点的索引号</td>
   </tr>
   <tr>
      <td>index</td>
      <td>string</td>
      <td>1</td>
      <td>分词的索引号</td>
   </tr>
   <tr>
      <td>word</td>
      <td>string</td>
      <td>克林顿</td>
      <td>分词</td>
   </tr>
</table>

 
### 2、返回示例    


```
{
    "code": "10000",
    "charge": false,
    "remain": 0,
    "msg": "查询成功",
    "result": {
        "status": 0,
        "request_id": "6caf500a-4cc5-482e-996c-6c9808952c65",
        "message": "ok",
        "dependencyList": [
            {
                "dependencyRelation": "nsubj",
                "parent": "2",
                "index": "1",
                "word": "克林顿"
            },
            {
                "dependencyRelation": "root",
                "parent": "0",
                "index": "2",
                "word": "访问"
            },
            {
                "dependencyRelation": "dobj",
                "parent": "2",
                "index": "3",
                "word": "中国"
            }
        ]
    }
}
```
 
