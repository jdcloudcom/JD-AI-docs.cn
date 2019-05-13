# 拍照购

## 一、接口描述 
### 1. 功能描述  
  拍照购（Snapshop）API为用户提供商品搜索的图像检索方案：用户上传包含物品的日常图片，经过后台服务器处理，返回与上传图片中某一主体视觉相似的商品列表。
### 2. 能力说明：  
  当前可以检索如下类目的商品：裙装、上衣、下衣、鞋靴、箱包、数码家电、食品饮料、玩具乐器、配饰、个护洗化、家居家装、图书、绿植。
### 3. 接口数据要求：  
> 1. 图片格式：Base64
> 2. 图片像素：最小 128*128  
> 3. 图片大小：小于 3M

### 4. 接口使用：  

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。


在获得使用权限后，您可使用已经封装好的SDK/参照[接口鉴权](../Operation-Guide/Authentication.md)规则进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md) 。 

## 二、请求说明
### 1. 接口地址 ：

```
https://aiapi.jdcloud.com/jdai/snapshop
```

### 2. 请求方式：  
https `post` aiapi.jdcloud.com/jdai/snapshop
### 3. 请求参数    

#### （1）header请求参数
业务请求参数

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
Content-Type | String | 是 | text/plain | 标准编码格式
Authorization | String | 是 | JDCLOUD2-HMAC-SHA256Credential=access... | 签名

#### （2）body请求参数
业务请求参数

>首次请求参数
```
imageBase64=xxx&channel_id=test&topK=50&multi_bboxes=true&skip_detect=true
```
其中，各参数定义如下

名称 | 类型 | 必填 | 示例值 | 描述
------|-----|-----|-----|-----
imgBase64 | String | 是 | imgBase64=/9j/4AAQSk... | 图片base64编码
channel_id | String | 是 | channel_id=test | 业务方识别码
topK | int | 否 | topK=50 | 返回商品列表个数（默认为50）
multi_bboxes | bool | 否 | multi_bboxes=true | 是否返回多个检测框商品

>用户触发请求参数(测试接口暂不提供此功能)
```
imageBase64=xxx&channel_id=test&topK=50&action_type=0&main_category_list=5|1&main_category_id=2&main_body_rectangle=10,10|700,900
```
其中，各参数定义如下

名称 | 类型 | 必填 | 示例值 | 描述
------|------|------|------|------
imgBase64 | String | 是 | imgBase64=/9j/4AAQSk...| 图片base64编码
channel_id | String | 是 | channel_id=xxxx | 业务方识别码
topK | int | 否 | topK=50 | 返回商品列表个数（默认为50）
action_type | int | 是 | action_type=0 | 输入可选0或者1, 操作选择 0:切换类目 1:重新框选
main_category_list | String | action_type=0情况下必填 | main_category_list=<br/>5&#124;1&#124;3&#124;14&#124;4&#124;2 | 类目相似度排序（由首次请求返回结果获得）
main_category_id | int | action_type=0情况下必填 | main_category_id=2 | 待切换到类目的id
main_body_rectangle | String | action_type=1情况下必填 | main_body_rectangle=<br/>10,10&#124;700,900 | 重新框选区域位置,结构为:<br/>左上角坐标x值(left),<br/>左上角坐标y值(top)&#124;<br/>右下角坐标x值(right),<br/>右下角坐标y值(bottom)


注意:1.若无action_type字段，用户触发请求无效; 2.channel_id=test 每日最大调用量为500次。

### 4、请求代码示例
建议您使用我们提供的SDK进行调用，SDK获取及调用方式详见[sdk的使用方法](../Operation-Guide/Use-Sdk.md)

## 三、返回说明
### 1、返回参数
#### （1）公共返回参数  

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
code | string | 1000 | 参见[错误码](Error-Code.md)-系统级错误码
charge | boolean | false 或 true | false：不扣费， true：扣费
remain | long | 1305 | 按天计算剩余调用次数
msg | string | 查询成功 | 参见[错误码](Error-Code.md)-系统级错误码
result | object | {...} | 查询结果

#### （2）业务返回参数
result参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
status| int | 0 | 参见[错误码](Error-Code.md)-业务级错误码
message | string | "Interface Succeed!" | 参见[错误码](Error-Code.md)-业务级错误码
channel_id | string | "test" | 业务方识别码（与输入相同）
query_id | string | "bd65b0d0541f4b2c729a08e7bf123ff7" | 用户请求query唯一标识字段
main_category_list | string | 5&#124;1&#124;3&#124;14&#124;4&#124;2&#124;0 | 类目预测排序，根据分类置信度排序
main_category_names | string | 配饰&#124;鞋靴&#124;数码家居&#124;其他&#124;食品饮料&#124;箱包&#124;服装| 与类目列表对应的中文名称
img_width | int | 800 | 图像宽度
img_height | int | 800 | 图像高度
dataValue|  object| {...}|  返回商品信息  

dataValue参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
rectangle | object | {...} | 商品框和商品类目信息
sims | array | [...] | 相似商品列表信息

rectangle参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
bottom | float | 986.351 | 商品框下方值（右下角坐标y值）
cls | int | 0 | 类目信息
clsName | string | "服装" | 返回结果类目中文名称
isUserRectangle | int | 0 | 是否是用户框选（暂不支持）
left | float | 305.181 | 商品框左侧值（左上角坐标x值）
right | float | 410.498 | 商品框右侧值（右下角坐标x值）
top | float | 12.641 | 商品框上方值（左上角坐标y值）

sims参数信息

名称 | 类型 | 示例值 | 描述
------|-----|-----|-----
cls | int | 0 | 返回结果类目信息
clsName | string | "服装" | 返回结果类目中文名称
detailUrl | string | "http://item.jd.com/30149050873.html" | 商品详情页信息（JD.COM）
detailAppUrl | string | "http://item.m.jd.com/product/27629434441.html" | APP端商品详情页
dis | float | 0.737 | 商品图与用户上传图像相似度距离
similarity | float | 0.1221 | 商品图与用户上传图像相似度 
imageUrl | string | "http://img14..."(页面原因未全部展示) | 商品主图jfs地址
skuId | unsigned long | 30149050873 | 商品sku ID
skuName | string | "鞋柜简约现代经济型鞋门厅柜<br/>组装 北欧玄关柜柚木色两门高组装" | 商品名称
skuPrice | string | "123.00" | 商品价格
wareLabel | string | "自营" | 有自营/非自营/京东物流/京东精选 四种商品销售渠道可供选择

### 2、返回示例    

```
{
    "code": "10000",
    "charge": false,
    "remain": 0,
    "msg": "查询成功",
    "result": {
        "img_width": 150,
        "query_id": "9a82757c75896fa4104568ae00c88031",
        "img_height": 150,
        "dataValue": [
            {
                "sims": [
                    {
                        "skuName": "德玛仕（DEMASHI）电热开水器商用奶茶店开水机 步进式热水机 35L全自动电脑调温款饮水机 KW-10SA",
                        "detailAppUrl": "https://item.m.jd.com/product/5801191.html",
                        "similarity": 0.07060305674065623,
                        "imageUrl": "https://img12.360buyimg.com/img/jfs/t25078/121/2682556871/255531/980e34df/5bec213aN2c3b653a.jpg",
                        "clsName": "数码家居",
                        "skuPrice": "1299.00",
                        "wareLabel": "京东精选",
                        "cls": 3,
                        "detailUrl": "https://item.jd.com/5801191.html",
                        "skuId": 5801191,
                        "dis": 0.5218308325022584
                    },
                    ...
                    {
                        "skuName": "宝马导航钢化膜18款新5系3系4系gt7系x1x3x5x6内改装屏幕保护膜 16-18年X1【高配大屏】2件5折",
                        "detailAppUrl": "https://item.m.jd.com/product/42237226782.html",
                        "similarity": 0.06679428287910891,
                        "imageUrl": "https://img1.360buyimg.com/img/jfs/t1/28452/39/8278/118565/5c7513d5E85ce27bc/7e7e2b3ae0b19f44.jpg",
                        "clsName": "数码家居",
                        "skuPrice": "116",
                        "wareLabel": "非自营",
                        "cls": 3,
                        "detailUrl": "https://item.jd.com/42237226782.html",
                        "skuId": 42237226782,
                        "dis": 0.5258005450168343
                    }
                ],
                "rectangle": {
                    "top": "7.17224884",
                    "left": "19.9679718",
                    "bottom": "140.801773",
                    "clsName": "数码家居",
                    "cls": 3,
                    "right": "132.511536",
                    "isUserRectangle": 0
                }
            }
        ],
        "main_category_names": "数码家居|箱包|其他|配饰|食品饮料|鞋靴|服装|手机|图书|绿植",
        "main_category_list": "3|2|14|5|4|1|0|6|7|8",
        "message": "Interface Succeed!",
        "channel_id": "test",
        "status": "0"
    }
}
```

## 四、调用实例

### postman实例

注意Content-Type设置为text/plain

### 1.首次请求

#### 1)单主体
```
channel_id=xxx(以实际上线ID为准)&&imgBase64=/9j...（页面原因，不予以全部展示）
```
#### 2)多主体
```
multi_bboxes=true&&channel_id=xxx(以实际上线ID为准)&&imgBase64=/9j...（页面原因，不予以全部展示）
```

#### 3)返回相似商品个数限制
```
topK=5&&channel_id=xxx(以实际上线ID为准)&&imgBase64=/9j...（页面原因，不予以全部展示）
```
注意：首次请求、用户触发请求均支持

### 2.用户触发请求

#### 1)切换搜索商品类目
 ```
action_type=0&&main_category_list=3|14|5|2|4|0|1&&main_category_id=0&&channel_id=xxx(以实际上线ID为准)&&imgBase64=/9j...（页面原因，不予以全部展示）
 ``` 
#### 2)更改框选区域
 ```
 action_type=1&&main_body_rectangle=20,20|400,400&&channel_id=xxx(以实际上线ID为准)&&imgBase64=/9j...（页面原因，不予以全部展示）
 ```
#### 3)更改框选区域的情况下切换商品类目
```
action_type=0&&main_category_list=0|1|14|2|5|3|4&&main_category_id=3&&main_body_rectangle=20,20|400,400&&channel_id=xxx(以实际上线ID为准)&&imgBase64=/9j...（页面原因，不予以全部展示）
```

注意：接口不保留任何信息，如果需要交互，请求端需保留部分信息，比如多主体切换情况下，需保留之前返回的多主体位置信息

## 五、版本迭代

版本 | 迭代说明
------|------
v0.0.2|增加字段：移动端详情页（detailUrl）、商品标签（wareLabel）；更新价格接口(skuPrice)
v0.0.5|增加channel_id为用户识别码
v0.0.7|dataValue类型更新为json array
v0.0.11|补全链接字段
v0.0.15|增加用户触发请求功能
v0.0.16|修复用户触发请求功能部分bug
v0.0.18|测试数据库更新
v0.0.19|取消图像转存功能、增加类目名称等字段、更新用户触发请求图像入参