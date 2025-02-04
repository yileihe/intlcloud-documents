## 简介
日志管理功能够记录对于指定源存储桶的详细访问信息，并将这些信息以日志文件的形式保存在指定的存储桶中，以实现对存储桶更好的管理。

在目标存储桶中，日志记录路径为：

```shell
目标存储桶/路径前缀{YYYY}/{MM}/{DD}/{time}_{random}_{index}.gz
```

日志每5分钟生成一次，一条记录为一行，每条记录包含多个字段，字段之间以`\t`分割，目前日志字段为：

| 字段序号 | 名 称         | 含 义                  | 示例                                                                        |
| :--------: | :---------------: | :-----------------------: | ----------------------------------------------------------------------------- |
| 1        | eventVersion    | 记录版本             | 1.00                                                                          |
| 2        | bucketName      | 存储桶名称          | examplebucket-1250000000                                                      |
| 3        | qcsRegion       | 请求地域             | ap-beijing                                                                    |
| 4        | eventTime       | 事件时间（请求结束时间，UTC 0时 时间戳） | 2018-12-01T11:02:33Z                                                          |
| 5        | eventSource     | 存储桶对应的域名 | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com                        |
| 6        | eventName       | 事件名称             | UploadPart                                                                    |
| 7        | remoteIp        | 来源 IP                 | 192.168.0.1                                                                   |
| 8        | userSecretKeyId | 用户访问 KeyId        | AKIDNYVCdoJQyGJ5brTf                                                          |
| 9        | reqQcsSource    | 请求 qcs 源信息       | qcs::cos:ap-beijing:uin/100000000001:examplebucket-1250000000/folder/text.txt |
| 10       | reqBytesSent    | 请求字节数（Bytes） | 83886080                                                                      |
| 11       | deltaDataSize   | 请求对存储量的改变（Bytes） | 12345678                                                                      |
| 12       | reqPath         | 请求的文件路径          | /folder/text.txt                                                              |
| 13       | reqMethod       | 请求方法             | put                                                                           |
| 14       | userAgent       | 用户 UA                | cos-go-sdk-v5.2.9                                                             |
| 15       | resHttpCode     | HTTP 返回码           | 200 OK                                                                        |
| 16       | resErrorCode    | 错误码                | No Content，目前暂不支持该字段，记录为‘-’                                         |
| 17       | resErrorMsg     | 错误信息             | SUCCESS                                                                       |
| 18       | resBytesSent    | 返回字节数（Bytes）   | 197                                                                           |
| 19       | resTotalTime    | 请求总耗时（毫秒，等于响应末字节的时间-请求首字节的时间） | 4295                                                                          |
| 20       | logSourceType   | 日志源类型          | COS                                                           |
| 21       | storageClass    | 存储类型             | STANDARD，STANDARD_IA，ARCHIVE                                              |
| 22       | accountid    | 存储桶所有者ID             | 100000000001                                              |
| 23       | resTurnAroundTime    | 请求服务端耗时（毫秒，等于响应首字节的时间-请求末字节的时间）             | 4295                                              |
| 24       | Requester    | 访问者             | 访问者账号昵称                                              |
| 25       | requestID    | 请求ID             | 本次请求的唯一ID                                              |
| 26       | objectSize    | 对象大小（Bytes）             | 账号                                              |
| 27       | versionid    | 对象版本ID             | 随机字符串                                              |
| 29       | targetStorageClass    | 目标存储类型，发起复制操作的请求会记录该字段             | STANDARD，STANDARD_IA，ARCHIVE                                              |
| 30       | syncRequest    | 是否腾讯云CDN回源请求             | Ture|
| 31       | referer    | 源站地址             | \*.example.com或者111.111.111.1                                              |

>!
> - 目前 COS 的日志管理功能仅支持北京、上海、广州、成都这四个地域。
> - 日志管理功能要求源存储桶与目标存储桶必须在同一地域。
> - 存放日志的目标存储桶可以是源存储桶本身，但不推荐。
> - 目前只有 XML API 以及基于 XML API 实现的 SDK、工具等进行的请求访问存储桶时，才会记录日志；JSON API 以及基于 JSON API 实现的 SDK、工具等进行的访问，不会记录日志。
> - 根据用户需求和业务发展情况，COS 可能在访问日志中新增字段，请在解析日志时务必做好相应处理。

## 启用日志管理
### 使用控制台
用户可以通过控制台快速开启日志管理功能。操作指引请参见 [设置日志管理](https://intl.cloud.tencent.com/document/product/436/17040) 控制台指南。

### 使用 API 
使用 API 为指定存储桶开启日志管理功能时，请参考以下步骤：
1. 创建日志角色。
2. 日志角色绑定权限。
3. 开启日志管理。

#### 1. 创建日志角色
创建日志角色，具体接口信息参见请 [CreateRole](https://intl.cloud.tencent.com/document/product/598/13886)。
其中，roleName 必须为：CLS_QcsRole。
policyDocument 为：

```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal": {
			"service": "cls.cloud.tencent.com"
		}
	}]
}
```
#### 2. 日志角色绑定权限
角色权限绑定权限，具体接口信息参见 [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/13889)。
其中，policyName 为：QcloudCOSAccessForCLSRole；roleName 为第1步中的 CLS_QcsRole，也可以使用创建 roleName 时返回的 roleID。

#### 3. 创建日志角色
调用接口，开启日志管理功能，具体接口信息请参见 [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/31483)，其中，要求存放日志的目标存储桶和源存储桶在同一地域。

