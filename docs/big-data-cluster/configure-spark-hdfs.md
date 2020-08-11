---
title: Apache Spark e Apache Hadoop
titleSuffix: Configure Apache Spark and Apache Hadoop in Big Data Clusters
description: Os Clusters de Big Data do SQL Server permitem as soluções Spark e HDFS. Saiba como configurá-los.
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.date: 02/21/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 34e7ae0ab570ea7a9480b2051aadb6140bb1c2ea
ms.sourcegitcommit: 22f687e9e8b4f37b877b2d19c5090dade8fa26d0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85334572"
---
# <a name="configure-apache-spark-and-apache-hadoop-in-big-data-clusters"></a>Configurar Apache Spark e Apache Hadoop em Clusters de Big Data

Para configurar o Apache Spark e o Apache Hadoop em Clusters de Big Data, você precisa modificar o perfil de cluster no momento da implantação.

Um cluster de Big Data tem quatro categorias de configuração: 

- `sql` 
- `hdfs` 
- `spark` 
- `gateway` 

`sql`, `hdfs`, `spark`, `sql` são serviços. Cada serviço é mapeado para a mesma categoria de configuração nomeada. Todas as configurações de gateway vão para a categoria `gateway`. 

Por exemplo, todas as configurações no `hdfs` de serviço pertencem à categoria `hdfs`. Observe que todas as configurações do Hadoop (core-site), HDFS e ZooKeeper pertencem à categoria `hdfs`. Todas as configurações de metastore do Livy, Spark, Yarn, Hive pertencem à categoria `spark`. 

Você pode encontrar todas as configurações possíveis para cada um no site de documentação associada do Apache:

- Apache Spark: https://spark.apache.org/docs/latest/configuration.html
- Apache Hadoop:
  - HDFS HDFS-Site: https://hadoop.apache.org/docs/r2.7.1/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml
  - HDFS Core-Site: https://hadoop.apache.org/docs/r2.8.0/hadoop-project-dist/hadoop-common/core-default.xml  
  - Yarn: https://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/ResourceModel.html
- Hive: https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties#ConfigurationProperties-MetaStore
- Livy: https://github.com/cloudera/livy/blob/master/conf/livy.conf.template
- Gateway Apache Knox: https://knox.apache.org/books/knox-0-14-0/user-guide.html#Gateway+Details

Além dessas configurações, também oferecemos a capacidade de configurar se os trabalhos do Spark podem ser executados no pool de armazenamento. 

Esse valor booliano, `includeSpark`, está no arquivo de configuração `bdc.json` em `spec.resources.storage-0.spec.settings.spark`.

## <a name="supported-configurations"></a>Configurações com suporte

O exemplo a seguir lista todas as configurações padrão para itens configuráveis compatíveis.

```json
{
  "hdfs": {
    "hdfs-site.dfs.replication": "2",
    "hdfs-site.dfs.ls.limit": "500",
    "hdfs-site.dfs.namenode.provided.enabled": "true",
    "hdfs-site.dfs.datanode.provided.enabled": "true",
    "hdfs-site.dfs.datanode.provided.volume.lazy.load": "true",
    "hdfs-site.dfs.provided.aliasmap.inmemory.enabled": "true",
    "hdfs-site.dfs.provided.aliasmap.class": "org.apache.hadoop.hdfs.server.common.blockaliasmap.impl.InMemoryLevelDBAliasMapClient",
    "hdfs-site.dfs.namenode.provided.aliasmap.class": "org.apache.hadoop.hdfs.server.common.blockaliasmap.impl.NamenodeInMemoryAliasMapClient",
    "hdfs-site.dfs.provided.aliasmap.load.retries": "10",
    "hdfs-site.dfs.provided.aliasmap.inmemory.batch-size": "1000",
    "hdfs-site.dfs.datanode.provided.volume.readthrough": "true",
    "hdfs-site.dfs.provided.overreplication.factor": "1",
    "hdfs-site.dfs.provided.cache.capacity.fraction": "0.01",
    "hdfs-site.dfs.provided.cache.capacity.mount": "true",

    "hdfs-env.HDFS_NAMENODE_OPTS": "-Dhadoop.security.logger=INFO,RFAS -Xmx2g",
    "hdfs-env.HDFS_DATANODE_OPTS": "-Dhadoop.security.logger=ERROR,RFAS -Xmx2g",
    "hdfs-env.HDFS_ZKFC_OPTS": "-Xmx1g",
    "hdfs-env.HDFS_JOURNALNODE_OPTS": "-Xmx2g",
    "hdfs-env.HDFS_AUDIT_LOGGER": "INFO,RFAAUDIT",

    "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "10",
    "core-site.fs.permissions.umask-mode": "077",
    "core-site.hadoop.security.kms.client.failover.max.retries": "20",

    "kms-site.hadoop.security.kms.encrypted.key.cache.size": "500",

    "zoo-cfg.tickTime": "2000",
    "zoo-cfg.initLimit": "10",
    "zoo-cfg.syncLimit": "5",
    "zoo-cfg.maxClientCnxns": "60",
    "zoo-cfg.minSessionTimeout": "4000",
    "zoo-cfg.maxSessionTimeout": "40000",
    "zoo-cfg.autopurge.snapRetainCount": "3",
    "zoo-cfg.autopurge.purgeInterval": "0",

    "zookeeper-java-env.JVMFLAGS": "-Xmx1G -Xms1G",
    
    "zookeeper-log4j-properties.zookeeper.console.threshold": "INFO"
  },
  "spark": {
    "capacity-scheduler.yarn.scheduler.capacity.maximum-applications": "10000",
    "capacity-scheduler.yarn.scheduler.capacity.resource-calculator": "org.apache.hadoop.yarn.util.resource.DominantResourceCalculator",
    "capacity-scheduler.yarn.scheduler.capacity.root.queues": "default",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.capacity": "100",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.user-limit-factor": "1",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.maximum-capacity": "100",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.state": "RUNNING",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.maximum-application-lifetime": "-1",
    "capacity-scheduler.yarn.scheduler.capacity.root.default.default-application-lifetime": "-1",
    "capacity-scheduler.yarn.scheduler.capacity.node-locality-delay": "40",
    "capacity-scheduler.yarn.scheduler.capacity.rack-locality-additional-delay": "-1",

    "hadoop-env.HADOOP_HEAPSIZE_MAX": "2048",

    "yarn-env.YARN_RESOURCEMANAGER_HEAPSIZE": "2048",
    "yarn-env.YARN_NODEMANAGER_HEAPSIZE": "2048",

    "mapred-env.HADOOP_JOB_HISTORYSERVER_HEAPSIZE": "2048",

    "hive-env.HADOOP_HEAPSIZE": "2048",

    "livy-conf.livy.server.session.timeout-check": "true",
    "livy-conf.livy.server.session.timeout-check.skip-busy": "true",
    "livy-conf.livy.server.session.timeout": "2h",
    "livy-conf.livy.server.yarn.poll-interval": "500ms",
    "livy-conf.livy.rsc.jars": "local:/opt/livy/rsc-jars/livy-api.jar,local:/opt/livy/rsc-jars/livy-rsc.jar,local:/opt/livy/rsc-jars/netty-all.jar",
    "livy-conf.livy.repl.jars": "local:/opt/livy/repl_2.11-jars/livy-core.jar,local:/opt/livy/repl_2.11-jars/livy-repl.jar,local:/opt/livy/repl_2.11-jars/commons-codec.jar",
    "livy-conf.livy.rsc.sparkr.package": "hdfs:///system/livy/sparkr.zip",

    "livy-env.LIVY_SERVER_JAVA_OPTS": "-Xmx2g",

    "spark-defaults-conf.spark.r.backendConnectionTimeout": "86400",
    "spark-defaults-conf.spark.pyspark.python": "python3",
    "spark-defaults-conf.spark.yarn.jars": "local:/opt/spark/jars/*",

    "spark-history-server-conf.spark.history.fs.cleaner.maxAge": "7d",
    "spark-history-server-conf.spark.history.fs.cleaner.interval": "12h",

    "spark-env.SPARK_DAEMON_MEMORY": "2g",
    "spark-env.PYSPARK_ARCHIVES_PATH": "local:/opt/spark/python/lib/pyspark.zip,local:/opt/spark/python/lib/py4j-0.10.7-src.zip",

    "yarn-site.yarn.log-aggregation.retain-seconds": "604800",
    "yarn-site.yarn.nodemanager.log-aggregation.compression-type": "gz",
    "yarn-site.yarn.nodemanager.log-aggregation.roll-monitoring-interval-seconds": "3600",
    "yarn-site.yarn.scheduler.minimum-allocation-mb": "512",
    "yarn-site.yarn.scheduler.minimum-allocation-vcores": "1",
    "yarn-site.yarn.nm.liveness-monitor.expiry-interval-ms": "180000",
    "yarn-site.yarn.nodemanager.container-executor.class": "org.apache.hadoop.yarn.server.nodemanager.LinuxContainerExecutor"
  },
  "gateway": {
    "gateway-site.gateway.httpclient.socketTimeout": "90s",
    "gateway-site.sun.security.krb5.debug": "false",
    "knox-env.KNOX_GATEWAY_MEM_OPTS": "-Xmx2g"
  }
}
```

As seções a seguir listam configurações não compatíveis.

## <a name="unsupported-spark-configurations"></a>Configurações `spark` não compatíveis

As configurações `spark` a seguir não são compatíveis e não podem ser alteradas no contexto do cluster de Big Data.

| Categoria  | Subcategoria               | Arquivo                       | Configurações não compatíveis                                              |
|-----------|----------------------------|----------------------------|-------------------------------------------------------------------------|
|           | yarn-site                  | yarn-site.xml              | yarn.log-aggregation-enable                                             |
|           |                            |                            | yarn.log.server.url                                                     |
|           |                            |                            | yarn.nodemanager.pmem-check-enabled                                     |
|           |                            |                            | yarn.nodemanager.vmem-check-enabled                                     |
|           |                            |                            | yarn.nodemanager.aux-services                                           |
|           |                            |                            | yarn.resourcemanager.address                                            |
|           |                            |                            | yarn.nodemanager.address                                                |
|           |                            |                            | yarn.client.failover-no-ha-proxy-provider                               |
|           |                            |                            | yarn.client.failover-proxy-provider                                     |
|           |                            |                            | yarn.http.policy                                                        |
|           |                            |                            | yarn.nodemanager.linux-container-executor.secure-mode.use-pool-user     |
|           |                            |                            | yarn.nodemanager.linux-container-executor.secure-mode.pool-user-prefix  |
|           |                            |                            | yarn.nodemanager.linux-container-executor.nonsecure-mode.local-user     |
|           |                            |                            | yarn.acl.enable                                                         |
|           |                            |                            | yarn.admin.acl                                                          |
|           |                            |                            | yarn.resourcemanager.hostname                                           |
|           |                            |                            | yarn.resourcemanager.principal                                          |
|           |                            |                            | yarn.resourcemanager.keytab                                             |
|           |                            |                            | yarn.resourcemanager.webapp.spnego-keytab-file                          |
|           |                            |                            | yarn.resourcemanager.webapp.spnego-principal                            |
|           |                            |                            | yarn.nodemanager.principal                                              |
|           |                            |                            | yarn.nodemanager.keytab                                                 |
|           |                            |                            | yarn.nodemanager.webapp.spnego-keytab-file                              |
|           |                            |                            | yarn.nodemanager.webapp.spnego-principal                                |
|           |                            |                            | yarn.resourcemanager.ha.enabled                                         |
|           |                            |                            | yarn.resourcemanager.cluster-id                                         |
|           |                            |                            | yarn.resourcemanager.zk-address                                         |
|           |                            |                            | yarn.resourcemanager.ha.rm-ids                                          |
|           |                            |                            | yarn.resourcemanager.hostname.*                                         |
|           | capacity-scheduler         | capacity-scheduler.xml     | yarn.scheduler.capacity.root.acl_submit_applications                    |
|           |                            |                            | yarn.scheduler.capacity.root.acl_administer_queue                       |
|           |                            |                            | yarn.scheduler.capacity.root.default.acl_application_max_priority       |
|           | yarn-env                   | yarn-env.sh                |                                                                         |
|           | spark-defaults-conf        | spark-defaults.conf        | spark.yarn.archive                                                      |
|           |                            |                            | spark.yarn.historyServer.address                                        |
|           |                            |                            | spark.eventLog.enabled                                                  |
|           |                            |                            | spark.eventLog.dir                                                      |
|           |                            |                            | spark.sql.warehouse.dir                                                 |
|           |                            |                            | spark.sql.hive.metastore.version                                        |
|           |                            |                            | spark.sql.hive.metastore.jars                                           |
|           |                            |                            | spark.extraListeners                                                    |
|           |                            |                            | spark.metrics.conf                                                      |
|           |                            |                            | spark.ssl.enabled                                                       |
|           |                            |                            | spark.authenticate                                                      |
|           |                            |                            | spark.network.crypto.enabled                                            |
|           |                            |                            | spark.ssl.keyStore                                                      |
|           |                            |                            | spark.ssl.keyStorePassword  
|           |                            |                            | spark.ui.enabled                                                        |
|           | spark-env                  | spark-env.sh               | SPARK_NO_DAEMONIZE                                                      |
|           |                            |                            | SPARK_DIST_CLASSPATH                                                    |
|           | spark-history-server-conf  | spark-history-server.conf  | spark.history.fs.logDirectory                                           |
|           |                            |                            | spark.ui.proxyBase                                                      |
|           |                            |                            | spark.history.fs.cleaner.enabled                                        |
|           |                            |                            | spark.ssl.enabled                                                       |
|           |                            |                            | spark.authenticate                                                      |
|           |                            |                            | spark.network.crypto.enabled                                            |
|           |                            |                            | spark.ssl.keyStore                                                      |
|           |                            |                            | spark.ssl.keyStorePassword                                              |
|           |                            |                            | spark.history.kerberos.enabled                                          |
|           |                            |                            | spark.history.kerberos.principal                                        |
|           |                            |                            | spark.history.kerberos.keytab                                           |
|           |                            |                            | spark.ui.filters                                                        |
|           |                            |                            | spark.acls.enable                                                       |
|           |                            |                            | spark.history.ui.acls.enable                                            |
|           |                            |                            | spark.history.ui.admin.acls                                             |
|           |                            |                            | spark.history.ui.admin.acls.groups                                      |
|           | livy-conf                  | livy.conf                  | livy.keystore                                                           |
|           |                            |                            | livy.keystore.password                                                  |
|           |                            |                            | livy.spark.master                                                       |
|           |                            |                            | livy.spark.deploy-mode                                                  |
|           |                            |                            | livy.rsc.jars                                                           |
|           |                            |                            | livy.repl.jars                                                          |
|           |                            |                            | livy.rsc.pyspark.archives                                               |
|           |                            |                            | livy.rsc.sparkr.package                                                 |
|           |                            |                            | livy.repl.enable-hive-context                                           |
|           |                            |                            | livy.superusers                                                         |
|           |                            |                            | livy.server.auth.type                                                   |
|           |                            |                            | livy.server.launch.kerberos.keytab                                      |
|           |                            |                            | livy.server.launch.kerberos.principal                                   |
|           |                            |                            | livy.server.auth.kerberos.principal                                     |
|           |                            |                            | livy.server.auth.kerberos.keytab                                        |
|           |                            |                            | livy.impersonation.enabled                                              |
|           |                            |                            | livy.server.access-control.enabled                                      |
|           |                            |                            | livy.server.access-control.*                                            |
|           | livy-env                   | livy-env.sh                | LIVY_SERVER_JAVA_OPTS                                                   |
|           | hive-site                  | hive-site.xml              | javax.jdo.option.ConnectionURL                                          |
|           |                            |                            | javax.jdo.option.ConnectionDriverName                                   |
|           |                            |                            | javax.jdo.option.ConnectionUserName                                     |
|           |                            |                            | javax.jdo.option.ConnectionPassword                                     |
|           |                            |                            | hive.metastore.uris                                                     |
|           |                            |                            | hive.metastore.pre.event.listeners                                      |
|           |                            |                            | hive.security.authorization.enabled                                     |
|           |                            |                            | hive.security.metastore.authenticator.manager                           |
|           |                            |                            | hive.security.metastore.authorization.manager                           |
|           |                            |                            | hive.metastore.use.SSL                                                  |
|           |                            |                            | hive.metastore.keystore.path                                            |
|           |                            |                            | hive.metastore.keystore.password                                        |
|           |                            |                            | hive.metastore.truststore.path                                          |
|           |                            |                            | hive.metastore.truststore.password                                      |
|           |                            |                            | hive.metastore.kerberos.keytab.file                                     |
|           |                            |                            | hive.metastore.kerberos.principal                                       |
|           |                            |                            | hive.metastore.sasl.enabled                                             |
|           |                            |                            | hive.metastore.execute.setugi                                           |
|           |                            |                            | hive.cluster.delegation.token.store.class                               |
|           | hive-env                   | hive-env.sh                

## <a name="unsupported-hdfs-configurations"></a>Configurações `hdfs` não compatíveis

As configurações `hdfs` a seguir não são compatíveis e não podem ser alteradas no contexto do cluster de Big Data.

| Categoria  | Subcategoria               | Arquivo                       | Configurações não compatíveis                                              |
|-----------|----------------------------|----------------------------|-------------------------------------------------------------------------|
|          | core-site                   | core-site.xml                 | fs.defaultFS                                          |
|          |                             |                               | ha.zookeeper.quorum                                   |
|          |                             |                               | hadoop.tmp.dir                                        |
|          |                             |                               | hadoop.rpc.protection                                 |
|          |                             |                               | hadoop.security.auth_to_local                         |
|          |                             |                               | hadoop.security.authentication                        |
|          |                             |                               | hadoop.security.authorization                         |
|          |                             |                               | hadoop.http.authentication.simple.anonymous.allowed   |
|          |                             |                               | hadoop.http.authentication.type                       |
|          |                             |                               | hadoop.http.authentication.kerberos.principal         |
|          |                             |                               | hadoop.http.authentication.kerberos.keytab            |
|          |                             |                               | hadoop.http.filter.initializers                       |
|          |                             |                               | hadoop.security.group.mapping.*                       |
|          | hadoop-env                  | hadoop-env.sh                 | JAVA_HOME                                             |
|          |                             |                               | HADOOP_CLASSPATH                                      |
|          | mapred-env                  | mapred-env.sh                 |                                                       |
|          | hdfs-site                   | hdfs-site.xml                 | dfs.namenode.name.dir                                 |
|          |                             |                               | dfs.datanode.data.dir                                 |
|          |                             |                               | dfs.namenode.acls.enabled                             |
|          |                             |                               | dfs.namenode.datanode.registration.ip-hostname-check  |
|          |                             |                               | dfs.client.retry.policy.enabled                       |
|          |                             |                               | dfs.permissions.enabled                               |
|          |                             |                               | dfs.nameservices                                      |
|          |                             |                               | dfs.ha.namenodes.nmnode-0                             |
|          |                             |                               | dfs.namenode.rpc-address.nmnode-0.*                   |
|          |                             |                               | dfs.namenode.shared.edits.dir                         |
|          |                             |                               | dfs.ha.automatic-failover.enabled                     |
|          |                             |                               | dfs.ha.fencing.methods                                |
|          |                             |                               | dfs.journalnode.edits.dir                             |
|          |                             |                               | dfs.client.failover.proxy.provider.nmnode-0           |
|          |                             |                               | dfs.namenode.http-address                             |
|          |                             |                               | dfs.namenode.httpS-address                            |
|          |                             |                               | dfs.http.policy                                       |
|          |                             |                               | dfs.encrypt.data.transfer                             |
|          |                             |                               | dfs.block.access.token.enable                         |
|          |                             |                               | dfs.data.transfer.protection                          |
|          |                             |                               | dfs.encrypt.data.transfer.cipher.suites               |
|          |                             |                               | dfs.https.port                                        |
|          |                             |                               | dfs.namenode.keytab.file                              |
|          |                             |                               | dfs.namenode.kerberos.principal                       |
|          |                             |                               | dfs.namenode.kerberos.internal.spnego.principal       |
|          |                             |                               | dfs.datanode.data.dir.perm                            |
|          |                             |                               | dfs.datanode.address                                  |
|          |                             |                               | dfs.datanode.http.address                             |
|          |                             |                               | dfs.datanode.ipc.address                              |
|          |                             |                               | dfs.datanode.https.address                            |
|          |                             |                               | dfs.datanode.keytab.file                              |
|          |                             |                               | dfs.datanode.kerberos.principal                       |
|          |                             |                               | dfs.journalnode.keytab.file                           |
|          |                             |                               | dfs.journalnode.kerberos.principal                    |
|          |                             |                               | dfs.journalnode.kerberos.internal.spnego.principal    |
|          |                             |                               | dfs.web.authentication.kerberos.keytab                |
|          |                             |                               | dfs.web.authentication.kerberos.principal             |
|          |                             |                               | dfs.webhdfs.enabled                                   |
|          |                             |                               | dfs.permissions.superusergroup                        |
|          | hdfs-env                    | hdfs-env.sh                   | HADOOP_HEAPSIZE_MAX                                   |
|          | zoo-cfg                     | zoo.cfg                       | secureClientPort                                      |
|          |                             |                               | clientPort                                            |
|          |                             |                               | dataDir                                               |
|          |                             |                               | dataLogDir                                            |
|          |                             |                               | 4lw.commands.whitelist                                |
|          | zookeeper-java-env          | java.env                      | ZK_LOG_DIR                                            |
|          |                             |                               | SERVER_JVMFLAGS                                       |
|          | zookeeper-log4j-properties  | log4j.properties (zookeeper)  | log4j.rootLogger                                      |
|          |                             |                               | log4j.appender.CONSOLE.*                              |

## <a name="unsupported-gateway-configurations"></a>Configurações `gateway` não compatíveis

As configurações `gateway` a seguir não são compatíveis e não podem ser alteradas no contexto do cluster de Big Data.

| Categoria  | Subcategoria               | Arquivo                       | Configurações não compatíveis                                              |
|-----------|----------------------------|----------------------------|-------------------------------------------------------------------------|
|          | gateway-site                | gateway-site.xml              | gateway.port                                          |
|          |                             |                               | gateway.path                                          |
|          |                             |                               | gateway.gateway.conf.dir                              |
|          |                             |                               | gateway.hadoop.kerberos.secured                       |
|          |                             |                               | java.security.krb5.conf                               |
|          |                             |                               | java.security.auth.login.config                       |
|          |                             |                               | gateway.websocket.feature.enabled                     |
|          |                             |                               | gateway.scope.cookies.feature.enabled                 |
|          |                             |                               | ssl.exclude.protocols                                 |
|          |                             |                               | ssl.include.ciphers                                   |

## <a name="configurations-via-cluster-profile"></a>Configurações por meio do perfil do cluster

No perfil de cluster, há recursos e serviços. No momento da implantação, podemos especificar as configurações de uma das duas maneiras: 

* Em primeiro lugar, no nível de recurso: 

   Os seguintes exemplos são os arquivos de patch para o perfil: 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.zookeeper.spec.settings", 
         "value": { 
           "hdfs": { 
             "zoo-cfg.syncLimit": "6" 
           } 
         } 
   }
   ```

   Ou: 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.gateway.spec.settings", 
         "value": { 
           "gateway": { 
             "gateway-site.gateway.httpclient.socketTimeout": "95s" 
           } 
         } 
   } 
   ```

* Em segundo lugar, no nível de serviço. Atribua vários recursos a um serviço e especifique as configurações para o serviço.

   Veja abaixo um exemplo do arquivo de patch para o perfil: 

   ```json
   { 
         "op": "add", 
         "path": "spec.services.hdfs.settings", 
         "value": { 
           “core-site.hadoop.proxyuser.xyz.users”: “*” 
           … 
        } 
   } 
   ```

O `hdfs` de serviço é definido como:

```json
{ 
  "spec": { 
   "services": { 
     "hdfs": { 
        "resources": [ 
          "nmnode-0", 
          "zookeeper", 
          "storage-0", 
          "sparkhead" 
        ], 
        "settings":{ 
          "hdfs-site.dfs.replication": "3" 
        } 
      } 
    } 
  } 
} 
```
 
> [!NOTE]
> Configurações de nível de recurso substituem configurações de nível de serviço. Um recurso pode ser atribuído a vários serviços.

## <a name="limitations"></a>Limitações

As configurações só podem ser especificadas no nível de categoria. Para especificar várias configurações com a mesma subcategoria, não podemos extrair o prefixo comum no perfil de cluster. 

```json
{ 
      "op": "add", 
      "path": "spec.services.hdfs.settings.core-site.hadoop", 
      "value": { 
        “proxyuser.xyz.users”: “*”, 
        “proxyuser.abc.users”: “*” 
     } 
} 
```

## <a name="next-steps"></a>Próximas etapas

- [Referência de `azdata`](reference-azdata.md)

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
