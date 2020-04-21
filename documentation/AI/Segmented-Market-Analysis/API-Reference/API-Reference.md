# 细分市场划分

## 一、接口描述

### 1. 功能描述
> 使用先进的AI技术对某品类下的市场进行细分，并结合京东零售的流量、销售和市场反馈数据，对细分市场进行描述和分析。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明：

对某个品类的消费市场进行划分，将该品类下所有商品划归到对应的细分市场，并给出该细分市场的名称和对应的信息。

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/marketSegmentationAnalyse
```

### 2. 请求方式：

https `get` aiapi.jdcloud.com/jdai/marketSegmentationAnalyse

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
      <td>name</td>
      <td>String</td>
      <td>对开门国产高端冰箱市场</td>
      <td>细分市场名称</td>
   </tr>
   <tr>
      <td>sku_count</td>
      <td>int</td>
      <td>280</td>
      <td>自营商品数量</td>
   </tr>
   <tr>
      <td>avg_price</td>
      <td>int</td>
      <td>4650</td>
      <td>平均价格</td>
   </tr>
   <tr>
      <td>view_count</td>
      <td>int</td>
      <td>13350000</td>
      <td>近三个月浏览数</td>
   </tr>
      <tr>
      <td>order_rate</td>
      <td>Float</td>
      <td>0.1160</td>
      <td>销量占比</td>
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
                    'sku_count': 280,
                    'avg_price': 4650,
                    'view_count': 13350000,
                    'order_rate': 0.116,
                    'name': '对开门国产高端冰箱市场',
                    'id': 0
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