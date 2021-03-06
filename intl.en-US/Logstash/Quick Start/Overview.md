# Overview

This topic describes how to quickly create an Alibaba Cloud Logstash cluster, configure Logstash pipelines, and synchronize data between Alibaba Cloud Elasticsearch clusters.

## Background information

Make sure that you have understood the following information:

-   [What is Alibaba Cloud Elasticsearch?](/intl.en-US/Product Introduction/What is Alibaba Cloud Elasticsearch?.md)
-   [What is Alibaba Cloud Logstash?](/intl.en-US/Logstash/What is Alibaba Cloud Logstash?.md)

## Procedure

1.  Make preparations.

    For more information, see [Preparations](). Preparations include creating a Virtual Private Cloud \(VPC\) and a VSwitch, creating source and destination Alibaba Cloud Elasticsearch clusters, enabling the Auto Indexing feature for the destination Alibaba Cloud Elasticsearch cluster, and preparing data.

2.  [Create an Alibaba Cloud Logstash cluster]().
3.  [Create and run a data synchronization task]().

    Create and configure an Alibaba Cloud Logstash pipeline to synchronize data.

4.  [View data synchronization results]().

    You can log on to the Kibana console of the destination Elasticsearch cluster to view the data synchronization results.


