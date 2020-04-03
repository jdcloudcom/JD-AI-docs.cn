# 通用图片搜索

## 一、接口描述

### 1. 功能描述
> 提供图片入库、入库图片搜索、图片及及信息管理等功能。

### 2. 接口使用

公测期间用户可以免费（0元）进行测试，根据[购买流程](../Pricing/Purchase-Process.md)下单后，即可开始体验业内领先的人工智能API服务。公测期间服务具有调用量、QPS限制，如需更高性能的API服务，请联系客服扩容购买。

在获得使用权限后，您可使用已经封装好的SDK进行相应开发，整体流程详见[调用方法](../Operation-Guide/call-methods.md)  。

### 3. 能力说明

> 基于检测、分类和特征表示能力，支持用户上传图片及相关信息后自动提取图片特征并构建索引，支持索引构建完成后进行图片搜索，图片及相关信息的管理。

## 二、请求说明
### [图片入库请求](./insert_data.html/)
### [任务状态查询请求](./fetch_task_status.html/)
### [图片搜索请求](./search.html/)
### [库列表查询请求](./list_collection.html/)
### [图片删除请求](./delete_image.html/)
### [图片信息更新请求](./update_infos.html/)
### [图片信息查询请求](./fetch_infos.html/)

## 三、接口数据要求
> 1. 图片格式：Base64 或 url
> 2. 图片像素：最小 201 \* 201，最大 4096 \* 4096
> 3. 图片大小：小于 3.75M
> 4. 图片类型：jpg, jpeg, png
> 5. 批量接口单次最大处理量为200

## 四、错误码

### 1.业务错误码

业务错误码（status）|对应message|说明
------|------|------
1004 | "TASK_NOT_EXIST" | 任务不存在
1030 | "NO_RELATIVE_COLLECTION" | 无相关的collection
1031 | "NO_RELATIVE_IMAGE" | 无相关的图片
1032 | "REPEAT_IMAGE_NAME_IN_DB" | 图片名与库中图片名重复
1033 | "REPEAT_IMAGE_NAME_IN_PARAM" | 参数列表中存在重复的图片名
2001 | "INVALID_PARAM_TOP_K" | 无效的top_k
2005 | "IMAGE_TOO_SMALL" | 图片大小超出最小限制
2006 | "BROKEN_BASE64_OR_URL" | 无效的base64或url
2007 | "IMAGE_TOO_LARGE" | 图片大小超出最大限制
2008 | "INVALID_DOCS" | 无效的入库数据
2010 | "INVALID_COLLECTION_NAME" | 无效的库名
2011 | "INVALID_IMAGE_INFO" | 无效的图片信息
2012 | "INVALID_IMAGE_NAME" | 无效的图片名
2013 | "COLLECTION_COUNT_EXCEEDS_LIMIT" | 超出允许创建的图片库数
2014 | "PARAMS_LENGTH_EXCEEDS_LIMIT" | 超过允许的参数长度
2015 | "COLLECTION_DOES_NOT_EXIST" | 该库不存在
5000 | "INTERNAL_SERVER_ERROR" | 内部服务错误