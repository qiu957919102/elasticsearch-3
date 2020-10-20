# DeleteConnectedCluster

Call DeleteConnectedCluster to remove the interconnected instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=elasticsearch&api=DeleteConnectedCluster&type=ROA&version=2017-06-13)

## Request header

This operation uses common request parameters only. For more information, see Common parameters.

## Request syntax

```
DELETE /openapi/instances/[InstanceId]/connected-clusters HTTPS|HTTP
```

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|connectedInstanceId|String|Yes|es-cn-09k1rgid9000g\*\*\*\*|The ID of the remote instance for which the network connection is established. |
|InstanceId|String|Yes|es-cn-n6w1o1x0w001c\*\*\*\*|The ID of the current instance. |
|clientToken|String|No|5A2CFF0E-5718-45B5-9D4D-70B3FF\*\*\*\*|A unique token generated by the client to guarantee the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5FFD9ED4-C2EC-4E89-B22B-1ACB6FE1D\*\*\*|The ID of the request. |
|Result|Boolean|true|Return results:

-   true: remove the interworking instance successfully
-   false: remove the interworking instance failed |

## Examples

Sample requests

```
DELETE /openapi/instances/es-cn-n6w1o1x0w001c****/connected-clusters? connectedInstanceId=es-cn-09k1rgid9000g**** HTTP/1.1
Common request header
```

Sample success responses

`XML` format

```
<Result>true</Result>
<RequestId>4EA9579E-12E6-420B-9518-575FFC76****</RequestId>
```

`JSON` format

```
{
    "Result": true,
    "RequestId": "4EA9579E-12E6-420B-9518-575FFC76****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/elasticsearch).
