# 品牌竞争力分析

## 一、接口描述

### 1. 功能描述
> 品牌竞争力分析是针对目标品牌，利用AI算法从品牌忠诚度、品牌市占率、品牌搜索量、品牌总销量、品牌美誉度和品牌知名度等对品牌的竞争力进行全面洞察分析
  ，为政府产业品牌升级及新品牌建设提供决策依据。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明：

（一）功能介绍

功能1：品牌竞争力分析——利用大数据、AI算法输出各品牌不同维度的评分
功能2：品牌综合排名——对每个品牌价值进行综合打分和排名

（二）产品优势

优势1：品牌齐全——支持京东商城绝大多数在售品牌
优势2：分析维度齐全——针对品牌的各个维度进行全面对比分析
优势3：打分模型精准——模型打分规则基于电商积累多年的业务经验沉淀而成，结果更加精准

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/brandCompeteAnalyse
```

### 2. 请求方式：

https `get` aiapi.jdcloud.com/jdai/brandCompeteAnalyse

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

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
      <td>page_size</td>
      <td>int</td>
      <td>否</td>
      <td>10</td>
      <td>分页参数，参数只能为 10, 20, 30，默认单次查询 10 条</td>
   </tr>
   <tr>
      <td>page_now</td>
      <td>int</td>
      <td>否</td>
      <td>1</td>
      <td>分页参数，参数只能为大于 0，小于 99999999 的数，默认为第一页值为 1</td>
   </tr>
   <tr>
      <td>category</td>
      <td>int</td>
      <td>是</td>
      <td>1</td>
      <td>品牌类目，暂时只开放冰箱品牌类目，冰箱品牌类目值为 1</td>
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
      <td>1</td>
      <td>参照四、错误码-业务码</td>
   </tr>
    <tr>
      <td>message</td>
      <td>string</td>
      <td>ok</td>
      <td>状态码描述</td>
   </tr>
    <tr>
      <td>result</td>
      <td>object</td>
      <td>{...}</td>
      <td>品牌竞争力分析查询结果</td>
   </tr>

</table>

##### result 参数信息

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>total</td>
      <td>int</td>
      <td>100</td>
      <td>查询结果总条数</td>
   </tr>
   <tr>
      <td>size</td>
      <td>int</td>
      <td>10</td>
      <td>当前查询条件下接口返回结果条数</td>
   </tr>
   <tr>
      <td>list</td>
      <td>List</td>
      <td>[{..}, ..]</td>
      <td>品牌竞争力分析结果列表</td>
   </tr>

</table>

##### list 参数信息

<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>id</td>
      <td>long</td>
      <td>1</td>
      <td>字段编号</td>
   </tr>
   <tr>
      <td>brandname_full</td>
      <td>String</td>
      <td>品牌名称（品牌英文名）</td>
      <td>品牌名</td>
   </tr>
   <tr>
      <td>brand_recognition_score</td>
      <td>Float</td>
      <td>20.0</td>
      <td>品牌知名度</td>
   </tr>
   <tr>
      <td>brand_reputation_score</td>
      <td>Float</td>
      <td>5.0</td>
      <td>品牌美誉度</td>
   </tr>
      <tr>
      <td>brand_marketvalue_score</td>
      <td>Float</td>
      <td>35.0</td>
      <td>品牌市占率</td>
   </tr>
      <tr>
      <td>brand_search_score</td>
      <td>Float</td>
      <td>10.0</td>
      <td>品牌搜索量</td>
   </tr>
      <tr>
      <td>brand_sale_score</td>
      <td>Float</td>
      <td>25.0</td>
      <td>品牌总销量</td>
   </tr>
      <tr>
      <td>brand_loyalty_score</td>
      <td>Float</td>
      <td>21.721543876823016</td>
      <td>品牌忠诚度</td>
   </tr>
      <tr>
      <td>brand_compete_score</td>
      <td>Float</td>
      <td>117.72154387682302</td>
      <td>品牌竞争力评分</td>
   </tr>
</table>

### 2、返回示例

```JSON
{
    "code": "10000",
    "charge": false,
    "remainTimes": 4998,
    "remainSeconds": -1,
    "msg": "查询成功",
    "result": {
        "code": 1,
        "message": "ok",
        "result": {
            "size": 10,
            "total": 235
            "list": [
                {
                    "brand_compete_score": 117.72154387682302,
                    "brand_loyalty_score": 21.721543876823016,
                    "brand_marketvalue_score": 35,
                    "brand_recognition_score": 20,
                    "brand_reputation_score": 5,
                    "brand_sale_score": 25,
                    "brand_search_score": 10,
                    "brandname_full": "品牌名称（品牌英文名）",
                    "id": 0
                },
                ...
            ]
        }
    }
}
```

### 3、业务错误码
<table>
   <tr>
      <th>业务码（code）</th>
      <th>message</th>
      <th>说明</th>
   </tr>
   <tr>
      <td>1</td>
      <td>"ok"</td>
      <td>接口调用成功</td>
   </tr>
   <tr>
      <td>40000</td>
      <td>"An unknown exception occurred."</td>
      <td>接口调用失败，内部服务错误</td>
   </tr>
   <tr>
      <td>1004</td>
      <td>"parameter error: {error reason}"</td>
      <td>参数错误，并返回错误原因</td>
   </tr>

</table>