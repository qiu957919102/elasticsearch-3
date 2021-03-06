# 配置和查看Grafana监控大屏

Grafana是一款跨平台的开源的度量分析和可视化工具，主要用于大规模指标数据的可视化展示。本文介绍如何配置Grafana公网地址访问白名单、获取Grafana的用户名和密码以及查看Grafana监控大屏。

-   创建阿里云Elasticsearch实例，版本为6.7.0，且内核版本为1.2.0及以上。

    创建实例的具体操作，请参见[创建阿里云Elasticsearch实例](/cn.zh-CN/快速入门/步骤一：创建实例/创建阿里云Elasticsearch实例.md)。

    如果内核版本低于1.2.0，可升级内核版本。具体操作，请参见[升级版本](/cn.zh-CN/ES实例/升级版本/升级版本.md)。

-   熟悉Grafana监控大屏的使用方法。更多信息，请参见[Grafana Dashboard](https://grafana.com/docs/grafana/latest/features/dashboard/dashboards/)。
-   开通高级监控报警服务。

    具体操作，请参见[步骤一：开通高级监控报警服务](/cn.zh-CN/高级监控报警/快速开始.md)。


## 配置Grafana公网地址访问白名单

Grafana仅支持公网访问，且默认情况下，所有公网都可以访问Grafana。如果您需要限制Grafana的访问来源，可通过配置公网地址访问白名单来实现。

1.  登录[阿里云Elasticsearch控制台](https://elasticsearch.console.aliyun.com/#/home)。

2.  在左侧导航栏，单击**高级监控报警**。

3.  单击**前往使用**。

4.  在**监控模块**页面的**Grafana**区域，单击**访问控制**。

5.  在**访问控制**页面，打开**启用访问控制**开关。

    **说明：** 启用访问控制后，只有添加到**公网地址访问白名单**中的IP地址才能访问监控大屏。

6.  在**公网地址访问白名单**中，输入您要添加的IP地址，单击**提交修改**。

    ![配置公网地址访问白名单](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9338935951/p132523.png)

    **说明：** 在添加**公网地址访问白名单**时，需要注意：

    -   支持添加单个或多个IP地址，以及IP地址段。多个IP地址使用英文逗号隔开。
    -   白名单格式为xx.xx.xx.xx或xx.xx.xx.xx/24，不支持0.0.0.0、0.0.0.0/1和xx.xx.xx.xx/0。
    -   最多可添加300个IP地址或IP地址段。

## 获取Grafana的用户名和密码

开通高级监控报警服务后，Grafana监控大屏默认会生成一个用户名和密码，此用户名和密码不支持修改，请妥善保管。

1.  在**监控模块**的**Grafana**区域，单击**用户管理**。

2.  在**用户管理**页面，获取用户名。

3.  单击**查看密码**，获取密码。

    ![获取密码](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9338935951/p132533.png)


## 查看Grafana监控大屏

1.  在**监控模块**的**Grafana**区域，单击**查看大屏**。

2.  输入Grafana服务的用户名和密码，查看监控大屏。

    Grafana监控大屏中默认展示该账号下，所有已开通高级监控报警服务的Elasticsearch实例中，索引（除系统索引）的[监控指标](/cn.zh-CN/高级监控报警/指标.md)变化曲线图。

    ![Grafana监控大屏](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4638935951/p132265.png)

3.  过滤监控项。

    您可以在监控大屏上方，输入待监控的**instanceId**、**ip**等，过滤监控项。

    ![过滤监控项](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9338935951/p132277.png)

    |参数|说明|
    |--|--|
    |**instanceId**|待监控的实例ID。|
    |**ip**|对应实例中，待监控的节点的IP地址。|
    |**index**|待监控的索引名称。输入索引名称后，系统会过滤出该索引下的数据。|
    |**shardId**|待监控的分片ID。|
    |**datasource**|Elasticsearch内置参数，不支持修改。|


