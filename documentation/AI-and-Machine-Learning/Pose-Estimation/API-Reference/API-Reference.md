# 人体关键点检测


## 一、接口描述 
### 1. 功能描述  
人体关键点检测API能够准确地估计出图片或视频中的人体14个主要关键点，包括：左右手肘、左右手腕、左右肩膀、头、脖子、左右脚踝、左右膝盖和左右臀等。进而能够在多个场景形式下，对站立、坐姿、运动多个姿态进行估计，从而实现对动作姿态的检测识别。可以用于游戏互动、视频直播、AR/VR、便携式可穿戴设备等场景下的人体姿态识别。

### 2. 能力说明：   
人体的矩形框边长建议不小于图片最短边边长的 1 / 10。例如图片为 1080*960 像素，则建议的最小人体框最短边尺寸为 96 像素。如果不满足此要求，则可能会影响识别精度。

### 3. 接口数据要求：  
- 图片格式：jpg、jpng、png、jfif
- 图片像素尺寸：最小 256\*256 像素，最大 4096\*4096 像素
- 图片文件大小：2M

### 4. 接口使用： 

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/pose_estimation
```

### 2. 请求方式：  
https `post` aiapi.jdcloud.com/jdai/pose_estimation

### 3. 请求参数  
#### （1）query请求参数  

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
      <td>muti_det</td>
      <td>int</td>
      <td>是</td>   
      <td>2</td>
      <td>单人姿态预测或多人姿态预测；当值为1时，实现单人姿态预测；当值为2时，实现多人姿态预测</td>
   </tr>
</table>


#### （2）header请求参数
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

#### （3）body请求参数
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
      <td>无</td>
      <td>binary</td>
      <td>必选</td>
      <td>无</td>
      <td>图片内容，传入图片</td>
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
      <td>OK</td>
      <td>参照四、错误码-业务错误码</td>
   </tr>
   <tr>
      <td>request_id</td>
      <td>string</td>
      <td>12345678</td>
      <td>便于双方定位问题</td>
   </tr>
   <tr>
      <td>det_num</td>
      <td>int</td>
      <td>14</td>
      <td>检测的关键点数，暂时支持14点检测；默认输出值为14</td>
   </tr>
   <tr>
      <td>used_time</td>
      <td>int</td>
      <td>198</td>
      <td>整个请求花费的时间，单位为毫秒</td>
   </tr>
   <tr>
      <td>det_info</td>
      <td>array</td>
      <td> [{"person_num":1,"node_info":[...]},{"person_num":2,"node_info":[...]}] </td>
      <td>检测点的信息数组，详情见det_info字段说明。当没有检测到人时，会返回[] </td>
   </tr>
</table>

#### det_info字段说明
<table>
   <tr>
      <th>名称</th>
      <th>类型</th>
      <th>示例值</th>
      <th>描述</th>
   </tr>
   <tr>
      <td>person_num</td>
      <td>int</td>
      <td>4</td>
      <td>多人检测时，图中检测人员的编号，按照检测出的头部关键点位置，从左往右依次从1开始编号；单人检测时，该值为1</td>
   </tr>
    <tr>
      <td>node_info</td>
      <td>list列表</td>
      <td>[x,y,score,node,x,y,score,node,……]</td>
      <td>x为关键点的横坐标，类型为int，y为关键点的纵坐标，类型为int，score为置信度，类型为float，node为节点名，类型为str。<br>
      node的值为: head(头部)、neck(脖子)、r_shoulder（右肩膀）、r_elbow(右手肘)、r_wrist(右手腕)、l_shoulder（左肩膀）、l_elbow(左手肘)、l_wrist(左手腕)、r_hip（右臀部）、r_knee(右膝盖)、r_ankle(右脚踝)、l_hip（左臀部）、l_knee(左膝盖)、l_ankle(左脚踝)</td>
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
            "request_id ": "1543813615.443506",
   			"message":"ok ",
   			"det_num": 14,
   			"status": 0,
   			"used_time": 306, 
   			"det_info": [
  			   	{
     			 "person_num": 1, 
      			"node_info": [
      			58, 
      			276, 
      			0.9998019337654114, 
      			"head", 
      			60, 
      			323, 
      			0.9998019337654114, 
      			"neck", 
      			16, 
     			337, 
      			0.9998019337654114, 
      			"r_shoulder", 
      			33, 
      			407, 
      			0.9998019337654114, 
      			"r_elbow", 
      			82, 
     		 	439, 
      			0.9998019337654114, 
      			"r_wrist", 
      			100, 
      			331, 
      			0.9998019337654114, 
      			"l_shoulder", 
      			112, 
      			391, 
      			0.9998019337654114, 
     			"l_elbow", 
      			119, 
      			433, 
      			0.9998019337654114, 
      			"l_wrist", 
      			34, 
      			433, 
      			0.9237196964835981, 
      			"r_hip", 
      			70, 
      			460, 
      			0.9998019337654114, 
      			"r_knee", 
      			90, 
      			558, 
      			0.9998019337654114, 
      			"r_ankle", 
      			96, 
      			413, 
      			0.9946802868011275, 
      			"l_hip", 
      			150, 
     			432, 
      			0.9998019337654114, 
      			"l_knee", 
      			185, 
      			514, 
      			0.9998019337654114, 
      			"l_ankle"
      			]
   				}
   			]
    }
}
```

	


