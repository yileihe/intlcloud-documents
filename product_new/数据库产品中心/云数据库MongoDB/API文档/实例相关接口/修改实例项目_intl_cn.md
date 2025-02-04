## 1. 接口描述 
本接口(ModifyMongoDBProject)用于修改实例所属项目。
接口请求域名：<font style='color:red'>mongodb.api.qcloud.com </font>

## 2. 输入参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href='https://intl.cloud.tencent.com/document/product/213/6976' title='公共请求参数'>公共请求参数</a>页面。其中，此接口的Action字段为ModifyMongoDBProject。

| 参数名称 | 是否必选 | 类型 | 描述 |
|:---------|---------|---------|---------|
| instanceIds.n | 是 | String |一个或者多个实例ID，n表示从0开始的数组下标。实例ID，可通过 [DescribeMongoDBInstances](https://intl.cloud.tencent.com//document/product/240/8312) 接口返回值中的 instanceId 获取。|
| projectId | 是 | Int | 项目ID,取值以用户账户>用户账户相关接口查询>[项目列表](https://intl.cloud.tencent.com/document/product/378/4400)返回的projectId为准 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 公共错误码，0表示成功，其他值表示失败。详见错误码页面的<a href='https://cloud.tencent.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81' title='公共错误码'>公共错误码</a>。 |
| message | String | 错误信息描述, 成功时，该值为空 |
| codeDesc | String | 业务侧错误码英文描述。成功时返回Success，错误时返回具体业务错误原因。 |

## 4. 错误码
以下错误码表列出了该接口的业务逻辑错误码。

| 错误代码 | 英文提示 | 错误描述 |
|---------|---------|---------|
|11050|InvalidParameter|业务参数错误|
|11056|InstanceNotExists|没有找到对应实例|
|11057|InstanceBeenLocked|实例正被其它流程锁定，暂时不能执行该操作|
|10702|InstanceStatusAbnormal|实例状态异常,暂时不能执行该操作（比如：流程中或已隔离或已删除）|

## 5. 示例
<pre>
  https://mongodb.api.qcloud.com/v2/index.php?Action=ModifyMongoDBProject
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
	&instanceIds.0=cmgo-6ozqe0uh
	&projectId=1001
</pre>
返回示例如下：
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success"
}

```