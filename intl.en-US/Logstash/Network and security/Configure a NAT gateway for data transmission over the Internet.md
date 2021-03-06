---
keyword: [Logstash access to the Internet, access to Logstash over the Internet]
---

# Configure a NAT gateway for data transmission over the Internet

This topic describes how to configure a Network Address Translation \(NAT\) gateway to connect Alibaba Cloud Logstash in a virtual private cloud \(VPC\) to the Internet.

-   A VPC and a vSwitch are created.

    For more information, see [Create an IPv4 VPC network](/intl.en-US/Quick Start/Create an IPv4 VPC network.md).

-   A Logstash cluster is created.

    For more information, see [Create an Alibaba Cloud Logstash cluster](/intl.en-US/Logstash/Quick Start/Step 1: Create a Logstash cluster/Create an Alibaba Cloud Logstash cluster.md).


1.  Log on to the [Alibaba Cloud Elasticsearch console](https://elasticsearch.console.aliyun.com/#/home).

2.  In the left-side navigation pane, click **Logstash Clusters**.

3.  In the top navigation bar, select a region. On the **Clusters** page, click the ID of the desired cluster.

4.  In the left-side navigation pane, click **Networks and Security**.

5.  In the **Network Settings** section, click **Configure NAT Gateway**.

    For more information about the descriptions and configurations of NAT gateways, see [Manage NAT gateways](/intl.en-US/User Guide/Manage NAT gateways.md). Destination Network Address Translation \(DNAT\) entries allow services on the Internet to send data to Logstash. Source Network Address Translation \(SNAT\) entries allow Logstash to access the Internet.

6.  On the NAT Gateway page, click Create NAT Gateway.

    When you create a NAT gateway, select the region and VPC where the Logstash cluster resides. For more information, see [Create a NAT gateway]().

7.  Associate an elastic IP address \(EIP\) with the NAT gateway.

    1.  On the NAT Gateway page, find the created NAT gateway and choose **![More](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8592986061/p98649.png)** \> **Bind Elastic IP Address** in the **Actions** column.

    2.  In the Bind Elastic IP Address panel, click the **Select from EIP List** tab.

        If no EIPs are available, click the **Allocate and Bind EIP to NAT Gateway** tab. Then, complete the configuration as prompted.

    3.  Select an EIP and click **OK**.

        **Note:** One NAT gateway can be associated with a maximum of 20 EIPs. Among these EIPs, a maximum of 10 pay-as-you-go EIPs can be associated and each of the pay-as-you-go EIPs supports a peak throughput of 200 Mbit/s. You can submit a ticket to increase the number of EIPs that can be associated.

8.  Create a DNAT entry.

    1.  On the NAT Gateway page, find the NAT gateway and click **Configure DNAT** in the **Actions** column.

    2.  On the **DNAT Table** page, click **Create DNAT Entry**.

    3.  In the **Create DNAT Entry** panel, configure parameters.

        ![Create a DNAT entry](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8592986061/p67462.png)

        |Parameter|Description|
        |---------|-----------|
        |**Public IP Address**|Select an available public IP address. **Note:** If a public IP address is already used to create an SNAT entry, the public IP address cannot be used to create a DNAT entry. |
        |**Private IP Address**|Click the **Manually Input** tab and enter the IP addresses of your Logstash nodes. You can obtain the IP address on the Basic Information page of the Logstash cluster.|
        |**Port Settings**|Choose a DNAT mapping method.         -   **All**: This method uses IP mapping and associates an EIP with the Logstash cluster. All requests destined for the public IP address are forwarded to the Logstash cluster.
        -   **Specific Port**: This method uses port mapping. The NAT gateway forwards the requests from the specified protocol and port to the specified port of the Logstash cluster.

If you choose **Specific Port**, you must specify **Public Port** \(the external port for port forwarding\), **Private Port** \(the internal port for port forwarding\), and **IP Protocol** \(the type of the protocol for port forwarding\). |
        |**Entry Name**|Enter a name for the DNAT entry. The name must be 2 to 128 characters in length and can contain digits, underscores \(\_\), and hyphens \(-\). It must start with a letter. |

    4.  Click **OK**.

9.  Create an SNAT entry.

    1.  Navigate to the NAT Gateway page. Find the NAT gateway and click **Configure SNAT** in the **Actions** column.

    2.  On the **SNAT Table** page, click **Create SNAT Entry**.

    3.  In the **Create SNAT Entry** panel, click **VSwitch Granularity** and configure parameters.

        ![Create an SNAT entry](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8592986061/p67464.png)

        |Parameter|Description|
        |---------|-----------|
        |**VSwitch**|Select a vSwitch from the VPC where the Logstash cluster resides. All ECS instances under the specified vSwitch can access the Internet by using the SNAT feature.|
        |**Public IP Address**|Select the public IP address that is used to access the Internet. You can select multiple public IP addresses to build an SNAT IP address pool. If you select multiple public IP addresses to build an SNAT IP address pool, make sure that each public IP address is added to the same EIP Bandwidth Plan instance. For more information, see [Associate an EIP with an EIP bandwidth plan](/intl.en-US/User Guide/Manage Pay-As-You-Go-billed EIPs/Associate an EIP with an EIP bandwidth plan.md). |

        For more information about the parameters, see [Create a SNAT entry to access the Internet](/intl.en-US/User Guide/Create a SNAT entry to access the Internet.md).

    4.  Click **OK**.


