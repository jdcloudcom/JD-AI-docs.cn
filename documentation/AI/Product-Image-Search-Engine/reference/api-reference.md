# 商品图片搜索

## 一、接口描述

### 1. 功能描述
> 提供商品图片入库、商品识别和搜索、以及图片信息管理等功能。

### 2. 接口使用

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明

基于检测、分类和特征表示能力，支持用户上传图片及相关信息后自动提取图片特征并构建索引，
维护商品和图片信息，支持索引构建完成后进行图片搜索，图片及相关信息的管理。提供在商品图片识别和搜索的专业能力。

#### 4. 服务流程
![整体流程介绍](../../../../image/AI-and-Machine-Learning/Product-Search-Engine/product-search.png)

## 二、请求说明

### [创建商品接口](../reference/create-product.md)
### [商品图入库接口](../reference/add-image.md)
### [入库状态查询接口](../reference/task-status.md)
### [商品图片搜索接口](../reference/product-search.md)
### [商品图片信息查询](../reference/image-info.md)
### [商品图片删除](../reference/delete-image.md)
### [商品删除](../reference/delete-product.md)

### 三、接口数据要求
* 图片格式：Base64 或 url，URL仅支持JFS格式
* 图片像素：最小 201 * 201，最大 4096 * 4096
* 图片大小：单张图片小于 3.75M
* 图片类型：jpg, jpeg, png
* 批量接口单次最大处理量为200
* 每个商品最多上传30张图片

### 四、注意事项
1. <font color=red>商品图片搜索服务的接口调用次数及QPS是所有接口共享的，即所有接口调动次数总数不能超过限额。</font>
1. 目前不支持jfs图片服务器以外的图片url作为入参。当有大规模数据入库时，为了防止带宽打满，可将图片上传至京东OSS，获得OSS链接后再批量传入。
1. 网关对传输大小有限制，不可传输超过5M的内容；
1. 目前每个用户仅支持建立1个商品库，每个库目前可以创建100000个商品，每个商品目前最多支持入库30张照片

## 五、错误码

### 1.业务错误码

业务错误码（status）|对应message|说明
------|------|------
1004 | "TASK_NOT_EXIST" | 任务不存在
1030 | "NO_RELATIVE_COLLECTION" | 无相关的collection
1031 | "NO_RELATIVE_IMAGE" | 无相关的图片
1032 | "REPEAT_IMAGE_NAME_IN_DB" | 图片名与库中图片名重复
1033 | "REPEAT_IMAGE_NAME_IN_PARAM" | 参数列表中存在重复的图片名
2001 | "INVALID_PARAM_TOP_K" | 无效的top_k
2006 | "BROKEN_BASE64_OR_URL" | 无效的base64或url
2005 | "IMAGE_TOO_SMALL" | 图片尺寸过小（小于201*201）
2007 | "IMAGE_TOO_LARGE" | 图片尺寸过大（大于4096*4096）
2008 | "INVALID_DOCS" | 无效的入库数据
2010 | "INVALID_COLLECTION_NAME" | 无效的库名
2011 | "INVALID_IMAGE_INFO" | 无效的图片信息
2013 | "COLLECTION_COUNT_EXCEEDS_LIMIT" | 商品库超过最大数量限制
3000 | "INVALID_PRODUCT_LIST" | 商品列表不合法
3001 | "PRODUCT_EMPTY" | 商品为空
3002 | "DUPLICATE_PRODUCT" | 重复的商品
3003 | "INVALID_PRODUCT_ID" | 无效的商品ID
3004 | "INVALID_PRODUCT_NAME" | 无效的商品名称
3005 | "INVALID_PRODUCT_CATEGORY" | 无效的商品类别
3006 | "EXISTING_PRODUCT" | 已存在的商品
3007 | "NOT_EXISTING_PRODUCT" | 不存在的商品
3008 | "INSERT_PRODUCT_ERROR" | 商品入库异常
3009 | "NO_MATCHED_PRODUCT" | 没有匹配的商品
3010 | "INVALID_IMAGE_LIST" | 不合法的商品图片列表
3011 | "EMPTY_IMAGE_LIST" | 空的商品图片列表
3012 | "DUPLICATE_IMAGE" | 重复的商品图片
3013 | "INVALID_IMAGE_ID" | 不合法的商品ID
3014 | "INVALID_IMAGE_CONTENT" | 不合法的图片
3015 | "INVALID_IMAGE_INFO" | 不合法的商品图片信息
3016 | "IMAGE_NUM_EXCEED_TOTAL_LIMIT" | 批量图片数量超过限制
3017 | "IMAGE_NUM_EXCEED_PER_PRODUCT_LIMIT" | 每个商品的图片量超过限制
3018 | "INSERT_IMAGE_ERROR" | 图片入库异常
3019 | "NO_VALID_IMAGE" | 无合法的商品图片
3021 | "INVALID_TASK_ID" | 非法的入库任务ID
3030 | "QUERY_TASK_STATUS_ERROR" | 查询入库任务状态异常
3031 | "SEARCH_PRODUCT_IMAGE_ERROR" | 查询商品图片异常
3032 | "DELETE_IMAGE_ERROR" | 删除商品图片异常
3033 | "QUERY_IMAGE_INFO_ERROR" | 查询商品图片信息异常
3034 | "DELETE_COLLECTION_ERROR" | 删除商品库异常
3040 | "INVALID_SEARCH_TOPK" | 非法的搜索返回数量
3041 | "SEARCH_TOPK_EXCEED_LIMIT" | 搜索返回数量超过限制
3050 | "INVALID_IMAGE_ID_LIST" | 非法的图片ID列表
3051 | "EMPTY_IMAGE_ID_LIST" | 空的图片ID列表
3052 | "DUPLICATE_IMAGE_ID" | 重复的图片ID
3053 | "NO_VALID_IMAGE_ID" | 无合法的图片ID
3054 | "NOT_SUPPORT_IMAGE" | 不支持的图片格式
3055 | "PRODUCT_NUM_EXCEED_LIMIT" | 商品数量超过限制
3056 | "IMAGE_SIZE_EXCEED_LIMIT" | 图片大小超过限制
5000 | "INTERNAL_SERVER_ERROR" | 内部服务错误
5001 | "INVALID_PARAMETER_JSON" | 错误的参数JSON格式
