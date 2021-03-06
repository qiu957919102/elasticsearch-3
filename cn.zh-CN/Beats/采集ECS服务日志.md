---
keyword: 安装采集器
---

# 采集ECS服务日志

通过采集器（Beats），您可以采集云服务器ECS（Elastic Compute Service）中的日志文件、网络数据、服务器指标等数据，发送到阿里云Elasticsearch或Logstash中，进行监控、分析等操作。本文以Filebeat为例，介绍如何配置ECS服务日志采集。

您已完成以下操作：

-   创建阿里云Elasticsearch实例或Logstash实例。

    具体操作，请参见[创建阿里云Elasticsearch实例](/cn.zh-CN/Elasticsearch/快速入门/步骤一：创建实例/创建阿里云Elasticsearch实例.md)和[创建阿里云Logstash实例](/cn.zh-CN/Logstash/快速入门/步骤一：创建实例/创建阿里云Logstash实例.md)。

-   开启Elasticsearch实例的自动创建索引功能。

    出于安全考虑，阿里云Elasticsearch默认不允许**自动创建索引**。但Beats采集ECS服务日志时，需要依赖该功能，因此如果**采集器Output**选择为**Elasticsearch**，需要开启**自动创建索引**功能。具体操作，请参见[开启自动创建索引](/cn.zh-CN/Elasticsearch/快速入门/步骤二：配置实例（可选）.md)。

-   创建ECS实例，且该ECS实例与Elasticsearch实例或Logstash实例处于同一专有网络下。

    创建实例时，请选择Aliyun Linux、RedHat或CentOS这三种操作系统，因为Beats仅支持这三种操作系统。具体操作，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

    **说明：** Beats默认安装目录为/opt/aliyunbeats/。安装后，ECS上会生成conf、logs和data这3个目录，分别映射了配置文件、Beats日志文件和Beats数据文件。建议不要删除或修改这3个文件中的内容，否则可能出现异常或者导致数据不正确。当出现问题时，您可以在logs目录下查看Beats日志来定位问题。

-   在目标ECS实例上安装云助手和Docker服务。

    具体操作，请参见[安装云助手客户端](/cn.zh-CN/运维与监控/云助手/配置云助手客户端/安装云助手客户端.md)、[部署并使用Docker（Alibaba Cloud Linux 2）](/cn.zh-CN/建站教程/搭建应用/部署并使用Docker/部署并使用Docker（Alibaba Cloud Linux 2）.md)。


## 操作步骤

1.  登录[阿里云Elasticsearch控制台](https://elasticsearch.console.aliyun.com/#/home)。

2.  在顶部菜单栏处，选择地域。然后在左侧导航栏，单击**Beats数据采集中心**。

    **说明：** 首次进入**Beats数据采集中心**，需要根据页面提示进行授权确认。

3.  配置并启动ECS服务日志采集。

    1.  在**创建采集器**区域，将鼠标移至**Filebeat**上，单击**ECS日志**。

        ![新建采集器页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5256461161/p76665.png)

        **说明：** 对于其他采集器，可直接单击采集器名称。例如创建Metricbeat采集器，可直接单击**Metricbeat**。

    2.  在**采集器配置**配置向导中，输入或选择采集器信息。完成后，单击**下一步**。

        ![采集器配置](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8242387951/p76666.png)

        |参数|说明|
        |--|--|
        |**采集器名称**|自定义输入采集器的名称。长度为1~30个字符，以大小写字母开头，可以包含字母、数字、下划线（\_）或连字符（-）。|
        |**安装版本**|目前Filebeat只支持**6.8.5**版本。|
        |**采集器Output**|Filebeat采集内容的输出地址。直接关联已经创建的阿里云Elasticsearch或Logstash实例。访问协议需要与所选Elasticsearch实例保持一致。|
        |**用户名密码**|如果**采集器Output**选择**Elasticsearch**，需要提供对应的用户名和密码，使Filebeat有权限向Elasticsearch实例中写入数据。用户名默认为elastic，密码在创建实例时设定，如果忘记可重置。重置密码的注意事项和操作步骤，请参见[重置实例访问密码](/cn.zh-CN/Elasticsearch/安全配置/重置实例访问密码.md)。|
        |**启用Monitoring**|用来监控Filebeat的相关指标。如果**采集器Output**选择**Elasticsearch**，Monitor默认使用和**采集器Output**相同的阿里云Elasticsearch实例；如果**采集器Output**选择**Logstash**，则需要在配置文件中进行额外配置。|
        |**启用Kibana Dashboard**|用来配置默认的Kibana Dashboard。由于阿里云Kibana配置在VPC内，因此需要在Kibana配置页面开通Kibana私网访问功能。具体操作，请参见[配置Kibana公网或私网访问白名单](/cn.zh-CN/Elasticsearch/可视化控制/Kibana/配置Kibana公网或私网访问白名单.md)。|
        |**填写Filebeat文件目录**|Filebeat专有的配置项。由于阿里云采用Docker部署Beats，因此需要将您希望采集的目录映射到Docker内，建议与filebeat.yml中的`input.path`保持一致。|
        |**采集器YML配置**|采集器配置文件。请根据业务需求，修改采集器YML文件的配置，详情请参见[采集器YML配置](/cn.zh-CN/Beats/采集器YML配置.md)。|

        **说明：** 指定**采集器Output**后，不需要再在**采集器YML配置**中单独设置Output，否则会提示ECS采集器安装错误。

    3.  在**采集器安装**配置向导中，选择需要操作的ECS实例。

        ![采集器安装](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8242387951/p76673.png)

        **说明：** 采集器安装实例列表中会显示当前账号下，所有和**采集器Output**所选的Elasticsearch实例或Logstash实例处于同一个专有网络下的ECS，并且只有已经安装云助手及Docker服务的ECS才能安装采集器。

    4.  单击**启动**。

    5.  在**启动成功**对话框中，单击**前往采集中心查看**。在采集器列表中，查看创建成功的采集器。

        等待**采集器状态**变为**已生效**，说明采集器创建成功。**已生效**中的两个数字分别表示安装成功的ECS数和目标ECS数，如果ECS实例生效成功，则两边数字相等。

        ![已生效采集器状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9242387951/p76692.png)

4.  查看运行实例。

    采集器创建成功后，您可以查看运行实例，判断采集器是否安装成功，并根据提示处理异常情况。

    1.  在**采集器管理**区域，单击对应采集器右侧**操作**列下的**查看运行实例**。

    2.  在**查看运行实例**页面，查看**采集器安装情况**。

        **采集器安装情况**分为3种：**心跳正常**、**心跳异常**、**安装失败**。在**心跳异常**或者**安装失败**的情况下，您可以选择移除或者重试问题节点。如果重试失败，可参见[Beats安装失败的排查与解决方法]()排查解决。

        ![查看运行实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9242387951/p76696.png)

    3.  单击**添加安装实例**，可继续添加需要安装同样配置和类型的采集器的ECS。

5.  查看Monitoring或Dashboard。

    如果您在创建采集器时勾选了**启用Monitoring**或**启用Kibana Dashboard**，那么Beats启动后，可以在对应Elasticsearch实例的Kibana中查看Monitor信息或Dashboard图表。

    1.  在**采集器管理**区域，单击对应采集器右侧**操作**列下的**更多** \> **查看Dashboard**。

    2.  在Kibana控制台登录页面，输入用户名和密码，单击登录。

    3.  在左侧导航栏，单击**Dashboard**，再单击对应指标，查看该指标的Dashboard图表。

        ![查看Dashboard图表](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9242387951/p76699.png)

    4.  在左侧导航栏，单击**Monitoring**，再单击对应监控项，查看该监控项的Monitoring信息。

        ![查看Monitoring信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9242387951/p76700.png)


