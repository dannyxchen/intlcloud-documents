## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (ModifyMigration) is used to modify the information of a migration task.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyMigration |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| MigrateId | Yes | Integer | Migration task ID |
| MigrateName | No | String | New name of the migration task. If this parameter is left empty, the migration task name will not be modified. |
| MigrateType | No | Integer | New migration type (1: structural migration, 2: data migration, 3: incremental synchronization). If this parameter is left empty, the migration type will not be modified. |
| SourceType | No | Integer | Type of the migration source. 1: CDB for SQLServer, 2: self-built SQLServer database on CVM, 4: SQLServer backup and restoration, 5: SQLServer backup and restoration (via COS). If this parameter is left empty, the type will not be modified. |
| Source | No | [MigrateSource](/document/api/238/19976#MigrateSource) | Migration source. If this parameter is left empty, the source will not be modified. |
| Target | No | [MigrateTarget](/document/api/238/19976#MigrateTarget) | Migration target. If this parameter is left empty, the target will not be modified. |
| MigrateDBSet.N | No | Array of [MigrateDB](/document/api/238/19976#MigrateDB) | The DB object for migration, which is not used for offline migration (SourceType=4 or SourceType=5). If this parameter is left empty, the DB object will not be modified. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| MigrateId | Integer | Migration task ID |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Modify a migration task

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=ModifyMigration
&MigrateId=2728
&MigrateName=Test API
&MigrateType=2
&SourceType=5
&Source.Url.0=http://gz-oncvm-1254065710.cosgz.myqcloud.com/testdb.bak
&Target.InstanceId=mssql-si2823jyl
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "MigrateId": 2728,
    "RequestId": "4be5990d-a4b5-49dc-b2b4-e713b6aa7ba3"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=ModifyMigration)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/238/19932#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.CreateFlowFailed | Failed to create a process |
| InternalError.DBError | Database error |
| InternalError.SystemError | System error |
| InternalError.UnknownError | Unknown error |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |
| ResourceNotFound.InstanceNotFound | Instance does not exist |
| ResourceUnavailable.InstanceMigrateRegionIllegal | Invalid region for instance migration |
| ResourceUnavailable.InstanceMigrateStatusInvalid | Invalid status of the instance migration task |
| ResourceUnavailable.InstanceStatusInvalid | Invalid instance status |

