## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (CreateLaunchConfiguration) creates a launch configuration.

* A few fields of a launch configuration can be modified through `ModifyLaunchConfigurationAttributes`. If you need to use a new launch configuration, we recommend you to create one.
* You can create up to 20 launch configurations for each project. For more information, see [Usage Limits](https://cloud.tencent.com/document/product/377/3120).


Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/30987).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateLaunchConfiguration |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/30987#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| LaunchConfigurationName | Yes | String | Name of the launch configuration. The name can be up to 60 bytes in size and contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points. |
| ImageId | Yes | String | Specify a valid [image](https://cloud.tencent.com/document/product/213/4940) ID in the format of `img-8toqc6s3`. There are four types of images: <br/><li>Public image </li><li>Custom image </li><li>Shared image </li><li>Service Market image </li><br/>The ID of an available image can be obtained in the following ways: <br/><li>Query the ID of a `public image`, `custom image`, or `shared image` in the [console](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE); query the ID of a `Service Market image` in the [Service Market](https://market.cloud.tencent.com/list). </li><li>Get the `ImageId` field in the return message after calling the [DescribeImages](https://cloud.tencent.com/document/api/213/15715) API. </li> |
| ProjectId | No | Integer | ID of the project to which the instance belongs. This parameter can also be obtained in the `projectId` field in the return value after calling the [DescribeProject](https://cloud.tencent.com/document/api/378/4400) API. If left blank, the default project. |
| InstanceType | No | String | Instance model. Different instance models specify different resource specifications. The specific value can be obtained by calling the [DescribeInstanceTypeConfigs](https://cloud.tencent.com/document/api/213/15749) API to get the latest specification table or referring to the descriptions in [Instance Types](https://cloud.tencent.com/document/product/213/11518). <br/>You must specify a value for either `InstanceType` or `InstanceTypes`. |
| SystemDisk | No | [SystemDisk](/document/api/377/31018#SystemDisk) | Information of the instance's system disk configuration. If this parameter is not specified, one is assigned according to the system default value. |
| DataDisks.N | No | Array of [DataDisk](/document/api/377/31018#DataDisk) | Information of the instance's data disk configuration. If this parameter is not specified, no data disk is purchased by default. Up to 11 data disks can be supported. |
| InternetAccessible | No | [InternetAccessible](/document/api/377/31018#InternetAccessible) | Information of the internet bandwidth configuration. If this parameter is not specified, the default internet bandwidth is 0 Mbps. |
| LoginSettings | No | [LoginSettings](/document/api/377/31018#LoginSettings) | Instance login settings. This parameter allows you to set the instance login password and key or keep the original login settings of the image. By default, the system will generate a random password and notify the user of it through internal messages. |
| SecurityGroupIds.N | No | Array of String | Security group of the instance. This parameter can be obtained in the `SecurityGroupId` field in the return value after calling the [DescribeSecurityGroups](https://cloud.tencent.com/document/api/215/15808) API. If this parameter is not specified, no security group is bound by default. |
| EnhancedService | No | [EnhancedService](/document/api/377/31018#EnhancedService) | Enhancement services. This parameter allows you to specify whether to enable services such as Cloud Security and Cloud Monitor. If this parameter is not specified, Cloud Monitor and Cloud Security are enabled by default. |
| UserData | No | String | Base64-encoded custom data of up to 16 KB. |
| InstanceChargeType | No | String | Instance billing type. CVM instances are POSTPAID_BY_HOUR by default. <br/><br><li>POSTPAID_BY_HOUR: Pay-as-you-go on an hourly basis <br/><br><li>SPOTPAID: Bidding |
| InstanceMarketOptions | No | [InstanceMarketOptionsRequest](/document/api/377/31018#InstanceMarketOptionsRequest) | Market-related options of the instance, such as the parameters related to stop instances. If the billing method of instance is specified as bidding, this parameter must be passed in. |
| InstanceTypes.N | No | Array of String | List of instance models. Different instance models specify different resource specifications. Up to 5 instance models can be supported. <br/>`InstanceType` and `InstanceTypes` are mutually exclusive, and one and only one of them must be entered. |
| InstanceTypesCheckPolicy | No | String | Instance type verification policy; valid values: ALL, ANY; ANY by default. <br/><br><li> ALL: The verification will success only if all instance types (InstanceType) are available; otherwise, an error will be returned. <br/><br><li> ANY: The verification will success if any instance type (InstanceType) is available; otherwise, an error will be returned. <br/><br/>Common reasons why an instance type is unavailable include runnng out of instance type or the corresponding cloud disk. <br/>If a model in InstanceTypes does not exist or has been discontinued, a verification error will be returned regardless of the value of InstanceTypesCheckPolicy. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| LaunchConfigurationId | String | ID of the launch configuration. This parameter is returned when a launch configuration is created through this API. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Creating a launch configuration using only the required parameters

Only assign values for the required parameters (launch configuration name, instance model, and image ID) and use system default values for other parameters. The specific configuration is as follows: launch configuration name: as_test, instance model: Standard II 1C1G (S2.SMALL1), image ID: img-8toqc6s3.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&InstanceType=S2.SMALL1
&ImageId=img-8toqc6s3
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "LaunchConfigurationId": "asc-23h37kyn",
        "RequestId": "d639dd64-9e46-4246-b13c-80954f81c11b"
    }
}
```

### Creating a lunch configuration using all parameters

Launch configuration name: as_test; image ID: img-8toqc6s3; model: Standard II 1C1G (S2.SMALL1); system disk: 50 GB local disk; data disk: 100 GB HDD cloud disk; internet billing method: pay-as-you-go by traffic on an hourly basis; upper limit for internet bandwidth: 5 Mbps; IP: public IP; login method: key; Cloud Monitor and Cloud Security: installed.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&ImageId=img-8toqc6s3
&InstanceType=S2.SMALL1
&SystemDisk.DiskType=LOCAL_BASIC
&SystemDisk.DiskSize=50
&DataDisks.0.DiskType=CLOUD_BASIC
&DataDisks.0.DiskSize=100
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=5
&InternetAccessible.PublicIpAssigned=TRUE
&LoginSettings.KeyIds.0=skey-k8eypc1l
&EnhancedService.SecurityService.Enabled=TRUE
&EnhancedService.MonitorService.Enabled=TRUE
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "LaunchConfigurationId": "asc-fdz8j7dh",
        "RequestId": "9a7209d3-2260-49d7-952a-dfa2001f8822"
    }
}
```

### Creating a Spot Instance Configuration

Launch configuration name: spot-test; model: Standard II 2C4G (S2.MEDIUM4); billing method: bidding (SPOTPAID); maximum bid: CNY0.99/hour.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=spot-test
&InstanceType=S2.MEDIUM4
&ImageId=img-8toqc6s3
&SystemDisk.DiskType=CLOUD_PREMIUM
&SystemDisk.DiskSize=50
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=20
&InternetAccessible.PublicIpAssigned=true
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.99
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "LaunchConfigurationId": "asc-hpzwe3o2",
        "RequestId": "ccfe3052-e9c9-47ee-bf3d-5bc2dfd972c0"
    }
}
```

### Creating a Launch Configuration That Supports Multiple Instance Models

This is to support two instance models, namely S2.SMALL2 and S2.SMALL4.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=multi_instance_types
&InstanceTypes.0=S2.SMALL2
&InstanceTypes.1=S2.SMALL4
&ImageId=img-8toqc6s3
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "LaunchConfigurationId": "asc-77mh1cho",
        "RequestId": "2864c860-27a0-439e-a1e1-0003b76734e7"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateLaunchConfiguration)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes,  see [Common Error Codes]

| Error Code | Description |
|---------|---------|
| AccountQualificationRestrictions | The requesting account failed to pass the qualification review. |
| CallCvmError | CVM API call failed. |
| InvalidImageId.NotFound | The image was not found. |
| InvalidLaunchConfiguration.NameDuplicate | The launch configuration name already exists. |
| InvalidParameter.Conflict | Parameters that cannot co-exist were specified. |
| InvalidParameter.MustOneParameter | The parameter is missing. You must specify at least one out of two parameter. |
| InvalidParameterValue.CvmConfigurationError | Exception with CVM parameter validation. |
| InvalidPermission | The account does not support this operation. |
| LaunchConfigurationQuotaLimitExceeded | The launch configuration quota is exceeded. |
