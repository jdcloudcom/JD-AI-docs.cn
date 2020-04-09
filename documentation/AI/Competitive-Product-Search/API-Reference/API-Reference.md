# 商品竞争力分析

## 一、接口描述

### 1. 功能描述
> 商品竞争力分析(commodity competitiveness analysis)API是针对目标商品在细分市场中的竞争情况的深度分
  析，从价格、品牌和商品属性等多维度对商品的竞争力进行全面洞察分析，辅助商家进行生产和营销策略的制定和调整，帮助商家了解已上市产品的竞对商品有哪些，以便进行生产和营销策略的制定和调整。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明：
输入SKU_ID品类限定为京东零售在售的自营冰箱品类，不能提供其他品类SKU_ID的识别能力。

### 4. 接口数据要求：
- sku_id：限定为京东零售在售自营冰箱品类sku_id

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/compete_analysis
```

### 2. 请求方式：

https `post` aiapi.jdcloud.com/jdai/compete_analysis

### 3. 请求参数

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|------|-----|-----|-----
Authorization | string | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名
Content-Type | String | 是 | application/x-www-form-urlencoded | 标准编码格式

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
      <td>self_flag</td>
      <td>boolean</td>
      <td>否</td>
      <td>是否剔除本品牌，示例self_flag=false </td>
      <td>默认不剔除本品牌，为false,不区分大小写</td>
   </tr>
   <tr>
      <td>show_count</td>
      <td>int</td>
      <td>否</td>
      <td>查找竞品数量，show_count= 3</td>
      <td>默认返回5个竞品信息，最大返回20个，若不足20个，则以返回值为准</td>
   </tr>
</table>

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
      <td>sku_id</td>
      <td>string</td>
      <td>是</td>
      <td>sku_id为京东零售在售自营冰箱品类sku,示例sku_id=2312215</td>
      <td>京东零售在售冰箱品类sku_id</td>
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
      <td>1000</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
   <tr>
      <td>message</td>
      <td>string</td>
      <td>success</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
   <tr>
      <td>res</td>
      <td>dict</td>
      <td>{...}</td>
      <td>返回竞品sku_id列表和对应竞争力得分列表</td>
   </tr>
</table>
res参数说明
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>sku_list</td>
      <td>dict</td>
      <td>{...}</td>
      <td>包含输入本品sku_id和竞品sku_id</td>
   </tr>
   <tr>
      <td>sku_compet_list</td>
      <td>list</td>
      <td>"sku_compet_list": ["1293744","100004013943"]</td>
      <td>返回竞品的sku_id列表</td>
   </tr>
   <tr>
      <td>input_sku_id</td>
      <td>string</td>
      <td>"input_sku_id": "2312215"</td>
      <td>输入的sku_id</td>
   </tr>
   <tr>
      <td>analysis_list</td>
      <td>list</td>
      <td>[...]</td>
      <td>竞品竞争能力值列表</td>
   </tr>
</table>
analysis_list参数说明
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>appear</td>
      <td>float</td>
      <td>58.00893422703027</td>
      <td>外观得分</td>
   </tr>
   <tr>
      <td>chara_fun</td>
      <td>float</td>
      <td>30</td>
      <td>特色功能得分</td>
   </tr>
   <tr>
      <td>basic_fun</td>
      <td>float</td>
      <td>100</td>
      <td>基本功能得分</td>
   </tr>
   <tr>
      <td>item_sku_id</td>
      <td>integer</td>
      <td>1293744</td>
      <td>sku_id</td>
   </tr>
   <tr>
      <td>price</td>
      <td>float</td>
      <td>100</td>
      <td>价格得分</td>
   </tr>
   <tr>
      <td>brand</td>
      <td>float</td>
      <td>30</td>
      <td>品牌得分</td>
   </tr>
</table>

### 2、返回示例

```JSON
{
    "code":1000,
    "charge":false,
    "remainTimes": 4998,
    "remainSeconds": -1,
    "msg":"查询成功",
    "result":{
         "res": {
                 "sku_list": {
                     "sku_compet_list": [
                         "1293744",
                         "100004013943",
                         "100007119438"
                     ],
                     "input_sku_id": "2312215"
                 },
                 "analysis_list": [
                     {
                         "appear": 58.00893422703027,
                         "chara_fun": 30,
                         "basic_fun": 100,
                         "item_sku_id": 1293744,
                         "price": 100,
                         "brand": 30
                     },
                     {
                         "appear": 100,
                         "chara_fun": 100,
                         "basic_fun": 43.62044659141338,
                         "item_sku_id": 100004013943,
                         "price": 58.82228690966849,
                         "brand": 30
                     },
                     {
                         "appear": 100,
                         "chara_fun": 100,
                         "basic_fun": 30,
                         "item_sku_id": 100007119438,
                         "price": 30,
                         "brand": 30
                     },
                     {
                         "appear": 30,
                         "chara_fun": 30,
                         "basic_fun": 100,
                         "item_sku_id": 2312215,
                         "price": 85.94744597006274,
                         "brand": 30
                     }
                 ]
             },
             "code": 1000,
             "message": "success"
    }
}
```

### 3、业务错误码
<table>
   <tr>
      <th>业务错误码（code）</th>
      <th>message</th>
      <th>说明</th>
   </tr>
   <tr>
      <td>1001</td>
      <td>"输入sku_id参数不正常"</td>
      <td>包括必选参数sku_id没填</td>
   </tr>
   <tr>
      <td>1002</td>
      <td>"输入show_count值超出范围"</td>
      <td>包括show_count值小于0或者大于20</td>
   </tr>
   <tr>
      <td>1003</td>
      <td>"接口返回值异常"</td>
      <td>包括输入异常和算法异常</td>
   </tr>
   <tr>
      <td>1004</td>
      <td>"self_flag参数无效"</td>
      <td>输入self_flag为非指定值</td>
   </tr>
</table>