# Elasticsearch服务关联角色

Elasticsearch服务关联角色（包括AliyunServiceRoleForElasticsearchOps和AliyunServiceRoleForElasticsearchCollector角色）是为了使用集群弹性扩缩容、创建和管理Beats采集器功能，需要获取其他云服务的访问权限，而提供的RAM角色。本文介绍阿里云Elasticsearch服务关联角色的应用场景，以及如何删除服务关联角色。

## 背景信息

关于服务关联角色的详细信息，请参见[服务关联角色](/cn.zh-CN/角色管理/服务关联角色.md)。

## 应用场景

AliyunServiceRoleForElasticsearchOps和AliyunServiceRoleForElasticsearchCollector角色的应用场景如下：

-   AliyunServiceRoleForElasticsearchOps

    执行[集群弹性扩缩容](/cn.zh-CN/ES实例/升降配实例/使用弹性扩缩功能.md)任务时，需要通过服务关联角色功能，授权阿里云Elasticsearch后台调用集群弹性扩缩容的OpenAPI，按照您设定的时间对集群扩缩容。

-   AliyunServiceRoleForElasticsearchCollector

    [创建和管理Beats采集器](/cn.zh-CN/Beats采集中心/安装采集器.md)时，需要通过服务关联角色功能，授权Beats采集器在云服务器ECS（Elastic Compute Service），或容器服务Kubernetes版ACK（Container Service for Kubernetes）的目标机器上，进行特定的管控操作。


## AliyunServiceRoleForElasticsearchOps介绍

当执行集群弹性扩缩容任务时，如果不存在具有执行任务权限的角色，Elasticsearch将自动创建对应角色（服务关联角色），并为该角色授予相应的权限。Elasticsearch通过扮演该角色即可调用OpenAPI，完成定时扩缩容任务。该角色的相关说明如下：

-   角色名称：AliyunServiceRoleForElasticsearchOps
-   角色权限策略名称：AliyunServiceRolePolicyForElasticsearchOps
-   角色权限策略内容：

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Action": [
            "elasticsearch:ListInstance",
            "elasticsearch:DescribeInstance",
            "elasticsearch:UpdateInstance",
            "elasticsearch:UpdateInstanceSettings",
            "elasticsearch:RestartInstance",
            "elasticsearch:RollbackInstance",
            "elasticsearch:DowngradeInstance",
            "elasticsearch:CancelTask",
            "elasticsearch:DeactivateZones",
            "elasticsearch:ActivateZones",
            "elasticsearch:MigrateToOtherZone",
            "elasticsearch:ResumeElasticsearchTask",
            "elasticsearch:InterruptElasticsearchTask",
            "elasticsearch:UpdateAdvancedSetting",
            "elasticsearch:UpgradeInstanceEngineVersion",
            "elasticsearch:UpdateWhiteIps",
            "elasticsearch:UpdatePublicIps",
            "elasticsearch:ModifyWhiteIps",
            "elasticsearch:TriggerNetwork",
            "elasticsearch:UpdateTemplate",
            "elasticsearch:DescribeLogstash",
            "elasticsearch:UpdateLogstash",
            "elasticsearch:RestartLogstash",
            "elasticsearch:UpdateLogstashSettings",
            "elasticsearch:InterruptLogstashTask",
            "elasticsearch:ResumeLogstashTask",
            "elasticsearch:DowngradeLogstash"
          ],
          "Resource": "*",
          "Effect": "Allow"
        }
      ]
    }
    ```

-   服务名称：ops.elasticsearch.aliyuncs.com
-   执行服务关联角色操作所需的用户权限：ram:CreateServiceLinkedRole

## AliyunServiceRoleForElasticsearchCollector介绍

创建和管理Beats采集器时，如果不存在具有执行任务权限的角色，Elasticsearch将自动创建对应角色（服务关联角色），并为该角色授予相应的权限。Elasticsearch通过扮演该角色即可调用OpenAPI，完成Beats采集器在ECS或ACK目标机器上的数据采集任务。该角色的相关说明如下：

-   角色名称：AliyunServiceRoleForElasticsearchCollector
-   角色权限策略名称：AliyunServiceRolePolicyForElasticsearchCollector
-   角色权限策略内容：

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Action": [
            "oos:CancelExecution",
            "oos:DeleteExecutions",
            "oos:GenerateExecutionPolicy",
            "oos:GetExecutionTemplate",
            "oos:ListExecutionLogs",
            "oos:ListExecutions",
            "oos:ListTaskExecutions",
            "oos:NotifyExecution",
            "oos:StartExecution",
            "oos:ListTagResources",
            "oos:TagResources",
            "oos:UntagResources",
            "oos:CreateTemplate",
            "oos:DeleteTemplate",
            "oos:GetTemplate",
            "oos:ListExecutionRiskyTasks",
            "oos:ListTemplates",
            "oos:UpdateTemplate"
          ],
          "Resource": "*",
          "Effect": "Allow"
        },
        {
          "Action": [
            "ecs:DescribeInstances",
            "ecs:DescribeCloudAssistantStatus"
          ],
          "Resource": "*",
          "Effect": "Allow"
        },
        {
          "Action": [
            "cs:GetUserConfig",
            "cs:GetClustersByUid",
            "cs:GetClusterInfo"
          ],
          "Resource": "*",
          "Effect": "Allow"
        },
        {
          "Action": "ram:DeleteServiceLinkedRole",
          "Resource": "*",
          "Effect": "Allow",
          "Condition": {
            "StringEquals": {
              "ram:ServiceName": "collector.elasticsearch.aliyuncs.com"
            }
          }
        },
        {
          "Effect": "Allow",
          "Action": "ram:PassRole",
          "Resource": "acs:ram:*:*:role/aliyunoosaccessingecs4esrole",
          "Condition": {
            "StringEquals": {
              "acs:Service": "oos.aliyuncs.com"
            }
          }
        }
      ]
    }
    ```

-   服务名称：collector.elasticsearch.aliyuncs.com
-   执行创建或删除服务关联角色操作所需的用户权限：ram:CreateServiceLinkedRole

## 删除服务关联角色

删除AliyunServiceRoleForElasticsearchOps服务关联角色，需要先停止依赖这个服务关联角色的Elasticsearch弹性扩缩容任务；删除AliyunServiceRoleForElasticsearchCollector服务关联角色，需要先删除依赖这个服务关联角色的所有Beats采集器。

删除服务关联角色的具体操作，请参见[删除服务关联角色](/cn.zh-CN/角色管理/服务关联角色.md)。

## 常见问题

Q：为什么我的RAM用户无法自动创建Elasticsearch服务关联角色？

A：主账号或拥有CreateServiceLinkedRole权限的RAM用户，才能自动创建或删除服务关联角色。因此当RAM用户无法自动创建服务关联角色时，需要通过主账号为其添加以下权限策略：

**说明：**

-   具体操作，请参见[为RAM用户授权](/cn.zh-CN/用户管理/为RAM用户授权.md)。
-   以下权限策略中的AccountId，需要替换为您的主账号ID。

-   AliyunServiceRoleForElasticsearchOps

    ```
    {
        "Statement": [
            {
                "Action": [
                    "ram:CreateServiceLinkedRole"
                ],
                "Resource": "acs:ram:*:${AccountId}:role/*",
                "Effect": "Allow",
                "Condition": {
                    "StringEquals": {
                        "ram:ServiceName": [
                            "ops.elasticsearch.aliyuncs.com"
                        ]
                    }
                }
            }
        ],
        "Version": "1"
    }
    ```

-   AliyunServiceRoleForElasticsearchCollector

    ```
    {
        "Statement": [
            {
                "Action": [
                    "ram:CreateServiceLinkedRole"
                ],
                "Resource": "acs:ram:*:${AccountId}:role/*",
                "Effect": "Allow",
                "Condition": {
                    "StringEquals": {
                        "ram:ServiceName": [
                            "collector.elasticsearch.aliyuncs.com"
                        ]
                    }
                }
            }
        ],
        "Version": "1"
    }
    ```


