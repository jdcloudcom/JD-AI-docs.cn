# 获取分组列表

----------

## 一、接口描述 

### 1.功能描述

获取用户的所有分组。

### 2. 接口使用 

公测期间用户可以免费（0元）进行测试，根据[购买流程](http://neuhub.jd.com/ai/api/face/search)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

使用接口前，需要先完成API的下单购买，然后可使用已经封装好的SDK/参照[接口鉴权](https://aidoc.jd.com/user/auth.html)规则进行相应开发，整体流程详见   [接入流程](https://aidoc.jd.com/user/flow.html)  。

## 二、请求说明

### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/getFaceGroupList
```

### 2. 请求方式：
  
https `post` aiapi.jdcloud.com/jdai/getFaceGroupList

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
      <td>start</td>
      <td>int</td>
      <td>是</td>
      <td>0</td>
      <td>查询起始位置</td>
   </tr>
   <tr>
      <td>length</td>
      <td>int</td>
      <td>是</td>
      <td>2</td>
      <td>从查询起始位置开始查询的长度，默认为5，最高值为5</td>
   </tr>

</table>

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](未发布)
 
## 返回说明

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
      <td>返回结果，0表示成功，非0为对应错误号</td>
   </tr>
   <tr>
      <td>message</td>
      <td>string</td>
      <td>Success</td>
      <td>若status为0，返回分组id，否则返回错误信息</td>
   </tr>
   <tr>
      <td>result</td>
      <td>string</td>
      <td></td>
      <td>分组列表</td>
   </tr>
</table>
 


### 2、返回示例

```Json
{
    "status": 0, 
    "charge": false,
    "remain": 97,
    "msg": "查询成功",
    "result": 
    {
{
    	    "result": "
    	    [
    	    {\"createTime\":1543415835000,
    	  \"groupId\":\"31270059-7698-4af1-82d5-7fd66ce772e1\",
    	    \"groupInfo\":\"test\",
    	    \"groupName\":\"test\",
    	    \"maxNumUser\":100000,
    	    \"subIndex\":1,
    	    \"updateTime\":1543415835000}
    	    ]",
    			"requestid": "081b1c5fe6dc465a9a54d75cedf78051",
    			"message": "success",
    			"status": 0
    }
    }
}
```
