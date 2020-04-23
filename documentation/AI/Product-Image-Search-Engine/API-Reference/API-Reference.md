# 商品图片搜索

## 一、接口描述

### 1. 功能描述
> 提供商品图片入库、商品识别和搜索、以及图片信息管理等功能。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明

基于检测、分类和特征表示能力，支持用户上传图片及相关信息后自动提取图片特征并构建索引，
维护商品和图片信息，支持索引构建完成后进行图片搜索，图片及相关信息的管理。提供在商品图片识别和搜索的专业能力。


## 二、请求说明

### [创建商品接口](create_product.md)
### [商品图入库接口](add_image.md)
### [入库状态查询接口](task_status.md)
### [商品图片搜索接口](product_search.md)
### [商品图片信息查询](image_info.md)
### [商品图片删除](delete_image.md)
### [商品删除](delete_product.md)

## 三、错误码

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
3019 | "NO_INVALID_IMAGE" | 无合法的商品图片
3020 | "INVALID_USER_ID" | 非法的用户ID
3021 | "INVALID_TASK_ID" | 非法的入库任务ID
3030 | "QUERY_TASK_STATUS_ERROR" | 查询入库任务状态异常
3031 | "SEARCH_PRODUCT_IMAGE_ERROR" | 查询商品图片异常
3031 | "DELETE_IMAGE_ERROR" | 删除商品图片异常
3033 | "QUERY_IMAGE_INFO_ERROR" | 查询商品图片信息异常
3034 | "DELETE_COLLECTION_ERROR" | 删除商品库异常
3040 | "INVALID_SEARCH_TOPK" | 非法的搜索返回数量
3041 | "SEARCH_TOPK_EXCEED_LIMIT" | 搜索返回数量超过限制
3050 | "INVALID_IMAGE_ID_LIST" | 非法的图片ID列表
3051 | "EMPTY_IMAGE_ID_LIST" | 空的图片ID列表
3052 | "DUPLICATE_IMAGE_ID" | 重复的图片ID
3053 | "NO_INVALID_IMAGE_ID" | 无合法的图片ID
3054 | "NOT_SUPPORT_IMAGE" | 不支持的图片格式
3055 | "PRODUCT_NUM_EXCEED_LIMIT" | 商品数量超过限制
3056 | "IMAGE_SIZE_EXCEED_LIMIT" | 图片大小超过限制
5000 | "INTERNAL_SERVER_ERROR" | 内部服务错误
5001 | "INVALID_PARAMETER_JSON" | 错误的参数JSON格式