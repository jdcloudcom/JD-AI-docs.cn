
# 错误码

### 1. 系统级错误码
<table>
  <tr>
    <th>返回码 (code)</th>
    <th>说明（message）</th>
  </tr>
    <tr>
      <td>10000</td>
      <td>查询成功</td>
    </tr>
  <tr>
    <td>10001</td>
    <td>错误的请求appkey</td>
  </tr>
  <tr>
    <td>10003</td>
    <td>不存在相应的数据信息</td>
  </tr>
  <tr>
    <td>10004</td>
    <td>URL上appkey参数不能为空</td>
  </tr>
    <tr>
      <td>10010</td>
      <td>接口需要付费，请充值</td>
    </tr>
   <tr>
    <td>10020</td>
    <td>系统繁忙，请稍后再试</td>
  </tr>
   <tr>
    <td>10030</td>
    <td>调用网关失败，请与NeuHub联系</td>
  </tr>
   <tr>
    <td>10040</td>
    <td>超过每天限量，请明天继续</td>
  </tr>
   <tr>
    <td>10041</td>
    <td>URL上timestamp参数不能为空</td>
  </tr>
   <tr>
    <td>10042</td>
    <td>URL上sign参数不能为空</td>
  </tr>
   <tr>
    <td>10043</td>
    <td>超过QPS限额，请降低调用频率或与NeuHub联系</td>
  </tr>
  <tr>
    <td>10044</td>
    <td>集群QPS超限额，请与NeuHub联系</td>
  </tr>
  <tr>
    <td>10045</td>
    <td>timestamp参数无效，请检查timestamp距离当前时间是否超过5分钟</td>
  </tr>
  <tr>
    <td>10046</td>
    <td>timestamp参数格式错误</td>
  </tr>
  <tr>
    <td>10047</td>
    <td>请求签名sign无效，请检查签名信息</td>
  </tr>
  <tr>
    <td>10048</td>
    <td>无接口权限，请下单购买</td>
  </tr>
  <tr>
    <td>10050</td>
    <td>用户已被禁用</td>
  </tr>   
  <tr>
    <td>10060</td>
    <td>发布方设置调用权限，请联系发布方</td>
  </tr>
  <tr>
    <td>11010</td>
    <td>发布方接口调用异常，请稍后再试</td>
  </tr>
  <tr>
    <td>11030</td>
    <td>发布方接口返回格式有误</td>
  </tr>  
</table>  


### 2. 业务错误码

<table>
   <tr>
      <th>业务错误码（status）</th>
      <th>对应message </th>
      <th>说明 </th>
   </tr>
   <tr>
      <td>12001</td>
      <td>"Invalid parameter"</td>
      <td>无效参数</td>
   </tr>
   <tr>
      <td>12002</td>
      <td>"Missing parameter"</td>
      <td>缺少参数</td>
   </tr>
   <tr>
      <td>12003</td>
      <td>"Error parsing parameter information"</td>
      <td>参数解析错误</td>
   </tr>
</table>



### 3. 网关系统级错误码

##### 表1.通用错误码
错误码| HTTP状态码| 错误信息| 解决方案
------|-----|-----|-----
ARGUMENT_NOT_SUPPORT | 400 | 参数 argument 不支持 | 请检查访问信息
ARGUMENT_NOT_FOUND |400|参数 argument 是必填参数|请检查访问信息
ARGUMENT_WRONG_FORMAT　|400	|参数 argument 类型应该是 某format	|请检查访问信息
OUT_OF_RANGE　|400|	参数取值不合法或超出范围	|请检查访问信息
ARGUMENT_MISMATCH|400|	资源 resource 不存在参数 argument|	请检查访问信息
INVALID_ARGUMENT	|400	|参数 argument 存在错误	|请检查访问信息
FAILED_PRECONDITION|	400	|资源 resource 在当前状态下不可进行当前操作|	请检查访问信息
UNAUTHENTICATED|	401	|认证失败	|请检查访问信息
HTTP_FORBIDDEN	|403|	没有对资源 resource 的 permission 权限|	请在相关系统或需联系相关管理员开权限
RESOURCE_NOT_EXIST	|404	|资源 resource 不存在|	请检查访问信息
NOT_FOUND	|404	|找不到 resource	|请检查访问信息
ABORTED	|409	|当前无法对 resource 进行操作	|请检查访问信息
ALREADY_EXISTS|	409|	resource 已存在	|请检查访问信息
CONFLICT|	409|	两种资源归属的父资源不一致	|请检查访问信息
FAILED_PRECONDITION|	409|	多个参数有大小依赖关系	|请检查访问信息
QUOTA_EXCEEDED|	429|	配额不足	|请检查访问信息，或增加配合
RATE_LIMIT_EXCEEDED|	429|	请求过频繁	|请稍后重试
CANCELLED|	499|	取消操作	
UNKNOWN|	500	|未知错误	|请稍后重试
INTERNAL|	500|	内部错误	|请稍后重试
NOT_IMPLEMENTED|	501|	目前不支持 method	|请检查访问信息
SOURCE_UNAVAILABLE|	502|	源站不可用	|请检查访问信息
UNAVAILABLE|	503|	服务不可用	|请检查访问信息
DEADLINE_EXCEEDED	|504|	超时	|请稍后重试

##### 表2.控制台错误码
错误码| HTTP状态码| 错误信息| 解决方案
------|-----|-----|-----
APIGATEWAY_SUCCESS|	200	|成功	|无
APIGATEWAY_ARGUMENT_NOT_SUPPORT	|400|	param 参数不支持	|请检查访问信息
APIGATEWAY_ARGUMENT_NOT_FOUND|	400|	param 不能为空	|请检查访问信息
APIGATEWAY_MODIFY_ERROR|	400	|该分组已发布，不能修改	|下线或者新建版本进行操作
APIGATEWAY_DELETE_API_ERROR	|400	|仍有上线版本，不能删除	|下线后才能删除
APIGATEWAY_NONE_VALID_PIN	|400	|无效的用户pin	|请检查访问信息
APIGATEWAY_DELETE_ERROR|	400	|未解除绑定，不能删除	|需要先解除所有分组的绑定关系，才能删除该项内容
APIGATEWAY_BIND_GROUP_TOO_MUCH|	400|	流控策略绑定分组多于一个	|如需进行下一步操作，需要先解除所有分组的绑定关系
APIGATEWAY_PATH_PARAMETERS_MUST_BE_DEFINED|	400|	请在查询参数Parameter Path中定义路径参数	|在查询参数Parameter Path中定义路径参数
APIGW_NO_HEADER	|400	|缺少header参数userId	|请检查访问信息
APIGW_PARAMS_NOT_EXIST	|400|	某参数不存在	|请检查访问信息
APIGW_PARAM_VALUE_INVALID	|400|	某参数不合法	|请检查访问信息
APIGW_RECORD_CONFLICT	|403	|已存在某参数	|请检查访问信息
APIGW_RECORD_NOT_FOUND	|404	|某参数不存在	|请检查访问信息
APIGATEWAY_BIND_GROUP_NOT_FOUND|	404|	访问授权与该分组不匹配|	请检查授权AK,SK是否已绑定该分组
APIGATEWAY_HTTP_FORBIDDEN	|403|	没有权限	|请在相关系统或需联系相关人员开权限
APIGATEWAY_DOMAIN_NO_RECORDED|403	|没有备案|	请先备案
APIGATEWAY_DOMAIN_ALREADY_EXISTS	|403|	域名已存在|	换一个
APIGATEWAY_DOMAIN_IS_BINDED|	403	|域名处于绑定状态，无法修改	|先解绑才能修改
APIGATEWAY_DOMAIN_NUM_IS_MAX	|403	|域名数量超过最大值	|请在最大范围内设置
APIGATEWAY_NONE_VALID_APPID	|404|	无效的keyID	|请检查访问信息
APIGATEWAY_NOT_FOUND	|404|	param 资源不存在	|请检查访问信息
APIGATEWAY_NONE_VALID_API	|404	|该分组没有有效的API	|请先创建API再进行下一步操作
APIGATEWAY_NOT_EXIST_METHOD_ERROR|	404	|不存在要验证的接口	|请检查访问信息
APIGATEWAY_SWAGGER_NULL_ERRO|	404|	yaml文件不能为空	|请检查访问信息
APIGATEWAY_APIGROUPNAME_ISREPEAT	|409|	分组名称重复	|请创建不重复内容
APIGATEWAY_BACKENDSERVICE_PREFIX_ISREPEAT|	409|	分组中后端服务前缀名重复	|请创建不重复内容
APIGATEWAY_APINAME_ISREPEAT	|409|	API名称重复	|请创建不重复内容
APIGATEWAY_ACCESSKEY_ISREPEAT	|409	|签名访问密钥重复	|请创建不重复内容
APIGATEWAY_ACCESSKEYAUTH_ISREPEAT	|409|	授权访问密钥重复	|请创建不重复内容
APIGATEWAY_POLICYNAME_ISREPEAT|	409	|策略名称重复	|请创建不重复内容
APIGATEWAY_API_PATH_ISREPEAT	|409|	API路径重复	|请创建不重复内容
APIGATEWAY_APISNAME_ISREPEAT	|409	|创建业务线分组名称重复	|请创建不重复内容
APIGATEWAY_REVISION_ISREPEAT	|409|	新增修订版本号重复	|请创建不重复内容
APIGATEWAY_SWAGGER_PARSE_ERROR	|500|	yaml文件解析异常	|请检查信息
APIGATEWAY_OPERATION_FAILED|	500	|操作失败	|请检查信息
APIGATEWAY_API_BODY_ERROR|	500	|要验证的接口的对应的body定义异常	|请检查信息
APIGATEWAY_INVALID_SERVICE_STATUS	|500|	服务未开通或已停止	|请检查信息
APIGATEWAY_INVALID_AUTHENTICATION_STATUS	|500|	该用户未进行实名认证	|请先实名认证
