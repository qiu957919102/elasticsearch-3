---
keyword: [Logstash third-party libraries, Logstash MySQL driver files]
---

# Configure third-party libraries

You can use the Third-party Libraries feature to upload driver files to the configuration file of an Alibaba Cloud Logstash cluster. The Third-party Libraries feature also allows you to manage the uploaded driver files.

1.  Log on to the [Alibaba Cloud Elasticsearch console](https://elasticsearch.console.aliyun.com/#/home).

2.  In the top navigation bar, select the region where your cluster resides.

3.  In the left-side navigation pane, click **Logstash Clusters**. On the page that appears, find the target cluster and click its ID in the **Cluster ID/Name** column.

4.  In the left-side navigation pane of the page that appears, click **Cluster Configuration**.

5.  In the **Third-party Libraries** section, click **Manage** next to **Upload**.

    ![Manage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1542986061/p69310.png)

6.  In the lower part of the **Modify Configuration** panel, click **Configure**.

7.  Click **Upload** and select the files that you want to upload.

    You can upload multiple driver files at a time. The file names must end with .jar, and each file name cannot exceed 100 characters in length. The system checks file names and MD5 checksum values before the files are uploaded. If the check fails, the system displays an error message, which indicates that the files cannot be uploaded.

    Logstash supports MySQL, PostgreSQL, and PolarDB JDBC driver files.

    |Driver type|Driver file|
    |-----------|-----------|
    |[MySQL JDBC driver](https://mvnrepository.com/artifact/mysql/mysql-connector-java)|    -   [mysql-connector-java-5.1.27.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.27/mysql-connector-java-5.1.27.jar)
    -   [mysql-connector-java-5.1.35.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.35/mysql-connector-java-5.1.35.jar)
    -   [mysql-connector-java-5.1.39-bin.jar](http://static.runoob.com/download/mysql-connector-java-5.1.39-bin.jar)
    -   [mysql-connector-java-5.1.39.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.39/mysql-connector-java-5.1.39.jar)
    -   [mysql-connector-java-5.1.43.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.43/mysql-connector-java-5.1.43.jar)
    -   [mysql-connector-java-5.1.47.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.47/mysql-connector-java-5.1.47.jar)
    -   [mysql-connector-java-5.1.48.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.48/mysql-connector-java-5.1.48.jar)
    -   [mysql-connector-java-5.1.9.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.9/mysql-connector-java-5.1.9.jar)
    -   [mysql-connector-java-6.0.2.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/6.0.2/mysql-connector-java-6.0.2.jar)
    -   [mysql-connector-java-6.0.6.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/6.0.6/mysql-connector-java-6.0.6.jar)
    -   [mysql-connector-java-8.0.11.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.11/mysql-connector-java-8.0.11.jar)
    -   [mysql-connector-java-8.0.17.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.17/mysql-connector-java-8.0.17.jar)
    -   [mysql-connector-java-8.0.18.jar](https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.18/mysql-connector-java-8.0.18.jar) |
    |[PolarDB JDBC driver]()|    -   [polardb-jdbc16.jar](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/33813/cn_zh/1594290740233/polardb-jdbc16.jar)
    -   [polardb-jdbc17.jar](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/33813/cn_zh/1594290803732/polardb-jdbc17.jar)
    -   [polardb-jdbc18.jar](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/33813/cn_zh/1594290862470/polardb-jdbc18.jar) |
    |[PostgreSQL JDBC driver](https://jdbc.postgresql.org/download.html)|    -   [postgresql-42.0.0.jar](https://jdbc.postgresql.org/download/postgresql-42.0.0.jar)
    -   [postgresql-42.1.4.jar](https://jdbc.postgresql.org/download/postgresql-42.1.4.jar)
    -   [postgresql-42.2.0.jar](https://jdbc.postgresql.org/download/postgresql-42.2.0.jar)
    -   [postgresql-42.2.1.jar](https://jdbc.postgresql.org/download/postgresql-42.2.1.jar)
    -   [postgresql-42.2.8.jar](https://jdbc.postgresql.org/download/postgresql-42.2.8.jar)
    -   [postgresql-42.2.10.jar](https://jdbc.postgresql.org/download/postgresql-42.2.10.jar)
    -   [postgresql-42.2.13.jar](https://jdbc.postgresql.org/download/postgresql-42.2.13.jar) |

    **Warning:** After you upload driver files for a cluster, the system restarts the cluster. This may affect your services. Therefore, proceed with caution.

8.  Click **Save**.

    After the files are uploaded, the system returns to the **Cluster Configuration** page and restarts the cluster. After the cluster is restarted, the third-party libraries are configured.

9.  Click **Manage** next to **Upload** to view the information about the third-party libraries in the **Modify Configuration** panel.

    The information about the third-party libraries contains **File** and **Path**.

    ![Modify Configuration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1542986061/p69324.png)

    **Note:**

    -   For security purposes, if you use a JDBC driver to configure a pipeline, you must add `allowLoadLocalInfile=false&autoDeserialize=false` at the end of the `jdbc_connection_string` parameter, such as `jdbc_connection_string => "jdbc:mysql://xxx.drds.aliyuncs.com:3306/test-database?allowLoadLocalInfile=false&autoDeserialize=false"`. Otherwise, the system displays an error message that indicates a check failure.
    -   To delete a file that you no longer use, go to the **Modify Configuration** panel, click **Configure** in the lower part, find the file, and then click the **X** icon.

