# **签名算法**

## **步骤1：创建标准请求串并加密**
首先要将请求按照下面的固定形式进行拼接，生成标准请求串。 示例伪代码

```
CanonicalRequest =
  HTTPRequestMethod + '\n' +
  CanonicalURI + '\n' +
  (CanonicalQueryString or '') + '\n' +
  CanonicalHeaders + '\n' +
  SignedHeaders + '\n' +
  Lowercase(HexEncode(Hash(RequestPayload or '')))
```
在此伪代码中：

HTTPRequestMethod即HTTP协议请求方式，如POST、GET等，使用全大写字母表示。

CanonicalURI即URI编码后的请求路径。

CanonicalQueryString为请求查询字符串。要构建规范查询字符串，首先按字符代码对***参数名按升序***进行排序，如果重复名称的参数再***按值升序***进行排序。然后对每个***参数名称和值分别进行URI编码***（请不要重复编码）。接着通过从排序列表中的第一个参数名称开始构建规范查询字符串。***对于每个参数，附加URI编码的参数名称，后跟等号字符（=），后跟URI编码的参数值***对没有值的参数使用空字符串。在每个参数值之后附加&符号，除了列表中的最后一个值。

要创建规范HTTP请求头列表，请将所有HTTP头名称转换为***小写***（请保证请求头名称不能包含空格），并***删除请求头value中前导空格和尾随空格。*** 通过用字符代码***升序***对请求头进行排序，然后遍历请求头名称来构建规范HTTP请求头列表。注意**：x-jdcloud-date**（遵循ISO8601标准，使用UTC时间，格式为YYYYMMDDTHHmmssZ）, ***x-jdcloud-nonce***必须在请求中包含并且参与签名；如果有***x-jdcloud-security-token***头，此项也必须参与签名。

CanonicalHeaders表示需要参与签名的请求头及值，使用:分隔名称和值，并添加换行符。 SignedHeaders用于告知京东云，请求头中的哪些是签名过程的一部分。

最后，需要把请求体中的payload做SHA256哈希后，表示为***小写十六进制字符串***。如果有效负载为空，则使用空字符串作为Hash函数的输入。

POST示例请求
```
POST
/v1/regions/cn-north-1/instances 

content-type:application/json
host:vm.jdcloud-api.com
x-jdcloud-date:20180404T034307Z
x-jdcloud-nonce:ed558a3b-9808-4edb-8597-187bda63a4f2 	

content-type;host;x-jdcloud-date;x-jdcloud-nonce
eadd64d9bd63436404495b9a2cd0a5b4c59b01332a88d81da27815824b3c4280
```
GET示例请求
```$xslt
GET
/v1/regions/cn-north-1/metrics/cpu_util/metricData
serviceCode=vm&startTime=2018-04-04T06%3A01%3A46Z
content-type:application/json
host:vm.jdcloud-api.com
x-jdcloud-date:20180404T061302Z
x-jdcloud-nonce:ed558a3b-9808-4edb-8597-187bda63a4f2 

content-type;host;x-jdcloud-date;x-jdcloud-nonce
eadd64d9bd63436404495b9a2cd0a5b4c59b01332a88d81da27815824b3c4280
```

## ***签名步骤2：生成待签名字符串***
要创建字符串进行签名，请连接规则请求的算法，日期和时间，凭据范围和摘要，如以下伪代码所示：
```$xslt
StringToSign =
Algorithm + \n +
RequestDateTime + \n +
CredentialScope + \n +
Lowercase(HexEncode(Hash(CanonicalRequest)))
```
其中，

Algorithm固定为JDCLOUD2-HMAC-SHA256是算法。

RequestDateTime与HTTP请求头x-jdcloud-date中的***格式和值必须完全一致。***

CredentialScope格式为”{时间}/{地域编码}/{产品线}/jdcloud2_request”，例如20180130/cn-north-1/vpc/jdcloud2_request

Lowercase(HexEncode(CanonicalRequest))是步骤1生成的标准请求进行***SHA256哈希***后，在表示为***小写十六进制字符串。***

例如：
```$xslt
JDCLOUD2-HMAC-SHA256
20180404T061302Z
20180404/cn-north-1/monitor/jdcloud2_request
5d7d08a5b792a63ad0bd820cff95ff41c6dbcf4bd7bae9e371be0ff891740ee7
```
## ***签名步骤3：计算签名***
计算的伪代码
```$xslt
kSecret = 京东云Access Key Secret
kDate = HMAC("JDCLOUD2" + kSecret, Date)
kRegion = HMAC(kDate, Region)
kService = HMAC(kRegion, Service)
kSigning = HMAC(kService, "jdcloud2_request")
```
其中HMAC(key, data)代表以二进制格式返回输出的HMAC-SHA256函数。散列过程中使用的日期格式为 YYYYMMDD，值必须与x-jdcloud-date中保持一致。Region表示地域编码，Service表示产品线名称。

使用生成的kSigning再对步骤2得到的待签名字符串进行HMAC运算,并将计算结果转为小写十六进制字符串：

```$xslt
signResult = Lowercase(HexEncode(HMAC(kSigning, StringToSign)))
```
最终生成一个签名串，如：
```
9b2026198d3acbf99da395e23a994ed369a0d70f5b4a5d7567dd0caf3009656d
```

## ***签名步骤4：向请求中添加签名信息***
计算签名后，需要将签名的结果作为Authorization请求头将其添加到请求中。

Authorization的格式为 JDCLOUD2-HMAC-SHA256 Credential={Access Key}/{Date}/{Region}/{Service}/jdcloud2_request, SignedHeaders={SignedHeaders}, Signature={signResult}

以curl命令调用方式的例子：
```$xslt
curl -X GET -H "x-jdcloud-date:20180404T061302Z" -H "x-jdcloud-nonce:ed558a3b-9808-4edb-8597-187bda63a4f2" -H "Authorization:JDCLOUD2-HMAC-SHA256 Credential=C61249XXXXXXXXXXXXXXXXXX/20180404/cn-north-1/monitor/jdcloud2_request, SignedHeaders=content-type;host;x-jdcloud-date;x-jdcloud-nonce, Signature=9b2026198d3acbf99da395e23a994ed369a0d70f5b4a5d7567dd0caf3009656d" -H "Content-Type:application/json" "http://vm.jdcloud-api.com/v1/regions/cn-north-1/metrics/cpu_util/metricData?serviceCode=vm&startTime=2018-04-04T06:01:46Z"
```

### ***签名步骤示例***
假设用户签名的输入信息为：

```$xslt
Access Key：'TESTAK'
Access Key Secret：'TESTSK'
Date：'20190214T104514Z'
Region：'cn-north-1'
Service：'test'
请求地址和路径：'http://test.jdcloud-api.com/v1/resource:action?p1=p1&p0=p0&o=%&u=u'
参与签名的请求头：
     'x-jdcloud-date' => '20190214T104514Z',
     'x-jdcloud-nonce' => 'testnonce',
     'x-my-header' => 'test',
     'x-my-header_blank' => ' blank'
请求地址和路径：'http://test.jdcloud-api.com/v1/resource:action?p1=p1&p0=p0&o=%&u=u'
请求体为： 'body data'
```
步骤1的结果应该为：

```$xslt
POST
/v1/resource%3Aaction
o=%25&p0=p0&p1=p1&u=u
x-jdcloud-date:20190214T104514Z
x-jdcloud-nonce:testnonce
x-my-header:test
x-my-header_blank:blank

x-jdcloud-date;x-jdcloud-nonce;x-my-header;x-my-header_blank
e51832a118eeff7ad976d635b7d04538e362e4c21bd0f6253580b0a83a209074
```
步骤2的结果应该为：
```$xslt
JDCLOUD2-HMAC-SHA256
20190214T104514Z
20190214/cn-north-1/test/jdcloud2_request
fb2e317056269590681d091f8eb22272967c0b922b2deda887312215ea4eed4c
```
步骤3的结果应该为：
```$xslt
（注意：kDate、kRegion、kService、kSigning应该是二进制格式的结果，下面展示的是转化为16进制字符串展示后的结果。这个只是为了页面展示目的，实际签名过程中，16进制的转化结果绝对不要作为下一步的输入，请使用原始二进制格式数据。）
kDate = dbbdee87f18afeedd6456923587f5323b90c3a77fbc6e381b243c90c672d5daf
kRegion = 78e1da51757851329da8e31a6bad9f509c4816cacb8d5b2b9d171e49498ce4b6
kService = 44050ec21c8e839f36ff5b2d44ec4a5876f4ffd6ef9a7a692a3eba40396bdb68
kSigning = a4e50bcb6001be0008696b173c30172b5ce22a77db00d21c6a9d69de2ba33b7d

signResult = 2a98f83c074e7bee260bfc8ef64f009c07595bd93f7f0c3f4e156bf6479ed9bf
```

步骤4的结果应该为：
```$xslt
JDCLOUD2-HMAC-SHA256 Credential=TESTAK/20190214/cn-north-1/test/jdcloud2_request, SignedHeaders=x-jdcloud-date;x-jdcloud-nonce;x-my-header;x-my-header_blank, Signature=2a98f83c074e7bee260bfc8ef64f009c07595bd93f7f0c3f4e156bf6479ed9bf
```