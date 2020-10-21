# UpdateHotIkDicts

Call UpdateHotIkDicts to update the IK dictionary for the Elasticsearch instance.

Note the following when you call this operation:

If the dictionary file is obtained through an OSS bucket, make sure that the OSS bucket is public-readable.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=elasticsearch&api=UpdateHotIkDicts&type=ROA&version=2017-06-13)

## Request header

This operation uses common request parameters only. For more information, see Common parameters.

## Request syntax

```
PUT /openapi/instances/[InstanceId]/ik-hot-dict HTTPS|HTTP
```

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|InstanceId|String|Yes|es-cn-oew1q8bev0002\*\*\*\*|The ID of the instance. |
|clientToken|String|No|5A2CFF0E-5718-45B5-9D4D-70B3FF\*\*\*\*|A unique token generated by the client to guarantee the idempotency of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## RequestBody

The following parameters must be set in RequestBody:

|Field

|Type

|Required

|Example

|Description |
|-------|------|----------|---------|-------------|
|name

|String

|Yes

|dic\_0.dic

|The name of the uploaded dictionary file. |
|ossObject

| |No

| |The description of the object that is stored in OSS. If the sourceType parameter is set to OSS, this parameter is required. |
|└bucketName

|String

|No

|search-cloud-test-cn-\*\*\*\*

|The name of the OSS bucket. |
|└key

|String

|No

|oss/dic\_0.dic

|The OSS path where the dictionary file is stored. |
|sourceType

|String

|Yes

|OSS

|Synonym source type that supports: OSS \(OSS open storage\), ORIGIN \(open source Elasticsearch\), UPLOAD \(the file that you UPLOAD\) . If the storage space is OSS, make sure that the OSS bucket is public-read. |
|type

|String

|Yes

|MAIN

|The dictionary type. Valid values: STOP, MAIN, SYNONYMS, and ALI\_WS. |

**Note:** └ indicates a child parameter.

Example:

```

[
    {
        "name":"deploy_0.dic",
        "ossObject":{
            "bucketName":"search-cloud-test-cn-****",
            "key":"user_dict/dict_0.dic"
        },
        "sourceType":"OSS",
        "type":"MAIN"
    },
    {
        "name":"SYSTEM_MAIN.dic",
        "type":"MAIN",
        "sourceType":"ORIGIN"
    },
    {
        "name":"SYSTEM_STOPWORD.dic",
        "type":"STOP",
        "sourceType":"ORIGIN"
    }
]
            
```

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Result|Array of DictList| |The return results. |
|fileSize|Long|6|Size of the synonym file in bytes. |
|name|String|ik\_main|The name of the object you want to upload. |
|sourceType|String|OSS|The type of the data source. |
|type|String|MAIN|Both MAIN and STOP parameters are supported.

-   MAIN:IK MAIN Dictionary
-   STOP:IK stopword Dictionary. |
|RequestId|String|5FFD9ED4-C2EC-4E89-B22B-1ACB6FE1\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
PUT /openapi/instances/es-cn-oew1q8bev0002****/ik-hot-dict HTTP/1.1
Common request parameters
[
    {
        "name":"deploy_0.dic",
        "ossObject":{
            "bucketName":"search-cloud-test-cn-****",
            "key":"user_dict/dict_0.dic"
        },
        "sourceType":"OSS",
        "type":"MAIN"
    },
    {
        "name":"SYSTEM_MAIN.dic",
        "type":"MAIN",
        "sourceType":"ORIGIN"
    },
    {
        "name":"SYSTEM_STOPWORD.dic",
        "type":"STOP",
        "sourceType":"ORIGIN"
    }
]
```

Sample success responses

`XML` format

```
<Result>
    <name>deploy_0.dic</name>
    <fileSize>220</fileSize>
    <sourceType>OSS</sourceType>
    <type>MAIN</type>
</Result>
<Result>
    <name>SYSTEM_MAIN.dic</name>
    <fileSize>2782602</fileSize>
    <sourceType>ORIGIN</sourceType>
    <type>MAIN</type>
</Result>
<Result>
    <name>SYSTEM_STOPWORD.dic</name>
    <fileSize>132</fileSize>
    <sourceType>ORIGIN</sourceType>
    <type>STOP</type>
</Result>
<RequestId>E1F6991B-1F77-47EA-9666-593F11E3****</RequestId>
```

`JSON` format

```
{
    "Result":[
        {
            "name":"deploy_0.dic",
            "fileSize":220,
            "sourceType":"OSS",
            "type":"MAIN"
        },
        {
            "name":"SYSTEM_MAIN.dic",
            "fileSize":2782602,
            "sourceType":"ORIGIN",
            "type":"MAIN"
        },
        {
            "name":"SYSTEM_STOPWORD.dic",
            "fileSize":132,
            "sourceType":"ORIGIN",
            "type":"STOP"
        }
    ],
    "RequestId": "E1F6991B-1F77-47EA-9666-593F11E3****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/elasticsearch).
