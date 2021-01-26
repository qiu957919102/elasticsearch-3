# DeleteDataTask

You can call this operation to delete an index migration task.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=elasticsearch&api=DeleteDataTask&type=ROA&version=2017-06-13)

## Request header

This operation uses only common request headers. For more information, see the Common request parameters topic.

## Request syntax

```
DELETE /openapi/instances/[InstanceId]/data-task HTTPS|HTTP
```

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|ClientToken|String|Yes|5A2CFF0E-5718-45B5-9D4D-70B3FF\*\*\*\*|A unique token generated by the client to guarantee the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|InstanceId|String|Yes|es-cn-oew1oxiro000f\*\*\*\*|The ID of the instance. |
|taskId|String|Yes|et\_cn\_0oyg09o96ib40\*\*\*\*|The ID of the index migration task. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5FFD9ED4-C2EC-4E89-B22B-1ACB6FE1D\*\*\*|The ID of the request. |
|Result|Boolean|true|The returned results. |

## Examples

Sample requests

```
DELETE /openapi/instances/es-cn-oew1oxiro000f****/data-task? taskId=et_cn_0oyg09o96ib40****&ClientToken=5A2CFF0E-5718-45B5-9D4D-70B3FF**** HTTP/1.1
Common request header
```

Sample success responses

`XML` format

```
<Result>true</Result>
<RequestId>3F71A6D2-7BD0-4A53-9119-386A2F0B****</RequestId>
```

`JSON` format

```
{
    "Result": true,
    "RequestId": "3F71A6D2-7BD0-4A53-9119-386A2F0B****"
}
```

## Error code

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/elasticsearch).
