# **sdk的使用方法**

## 获取说明 
根据[购买流程](未填超链接)，0元购买“智能鉴黄”产品后，再次进入京东云“智能鉴黄”控制台页面，点击[“下载SDK”](https://jdai.oss.cn-north-1.jcloudcs.com/aisdk/sdk/java.zip)，进入API调试页面下载SDK。

## 调用方式

## java示例代码
```$xslt
package com.jdcloud.apigateway.signature;

import java.io.UnsupportedEncodingException;
import java.util.Map;

import com.alibaba.fastjson.JSON;
import com.google.api.client.http.HttpResponse;
import com.google.api.client.util.Maps;

public class Main {

    public static void main(String[] args) throws UnsupportedEncodingException {
        String assessKey = "61C8C9D2178BC53592DBE7E37CB54BCA";
        String secretKey = "B7A9BE7D4EA1841F3B27AD130E8EFD26";
        String host = "xbgmzu559y83.cn-north-1.jdcloud-api.net:9000";
        String uri = "/v1/api/test";
        String method = "POST";
        Map<String, String> headers = Maps.newHashMap();
        headers.put("header1", "headerValue1");
        Map<String, Object> queryMap = Maps.newHashMap();
        queryMap.put("key1", "value1");
        String body = "{\"title\":\"qq\",\"description\":\"222\"}";
        HttpResponse httpResponse = JdcloudClient.execute(assessKey, secretKey, host, uri, method, headers, queryMap, body);
        System.out.println(JSON.toJSONString(httpResponse));
    }

}

```
java sdk[下载请点击](https://jdai.oss.cn-north-1.jcloudcs.com/aisdk/sdk/java.zip)


## python示例代码
```$xslt
# coding=utf8

from jdcloud_apim_sdk.core.credential import Credential
from jdcloud_apim_sdk.core.const import SCHEME_HTTPS, SCHEME_HTTP
from jdcloud_apim_sdk.core.config import Config
from jdcloud_apim_sdk.simpleclient import SimpleClient
from jdcloud_apim_sdk.simplerequest import SimpleRequest


if __name__=="__main__":
    access_key = 'ak'
    secret_key = 'sk'
    credential = Credential(access_key, secret_key)
    config = Config('xbgmzu559y83.cn-north-1.jdcloud-api.net:9000', scheme=SCHEME_HTTP, timeout=60)
    client = SimpleClient(config=config, credential=credential)

    parameters = dict()
    body = ''
    header = dict()

    simple_request = SimpleRequest('/v1/api/test', 'POST', parameters, body, header)
    response = client.send(simple_request)
    
```
python sdk[下载请点击](https://jdai.oss.cn-north-1.jcloudcs.com/aisdk/sdk/Python.zip)
