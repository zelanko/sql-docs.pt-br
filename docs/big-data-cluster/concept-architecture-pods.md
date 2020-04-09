---
title: Recursos implantados
titleSuffix: SQL Server Big Data Clusters
description: Uma descrição do pods normalmente implantados em um cluster de Big Data do SQL Server.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0cf0d79e08025d52b248175485ba2e3272e18dcb
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665457"
---
# <a name="resources-deployed-with-big-data-cluster"></a>Recursos implantados com o cluster de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve os recursos que o cluster de Big Data do SQL Server implanta.

Um cluster de Big Data implanta pods com base no perfil de implantação. Para saber detalhes, veja [Configurações padrão](deployment-guidance.md#configfile). 

Este artigo descreve os pods implantados com o perfil `aks-dev-test-ha` e inclui um pool do Spark. Consulte o Kubernetes para ver os pods implantados no cluster. O exemplo a seguir retorna uma lista de pods em um namespace específico.

```bash
kubectl get pods -n <namespace>
```

Substitua o `<namespace>` por um namespace do Kubernetes do cluster de Big Data. 

Para obter mais informações, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md#configfile).

O diagrama a seguir mostra os componentes implantados em um cluster de Big Data:

:::image type="content" source="media/big-data-cluster-overview/architecture-diagram-overview.png" alt-text="big-data-cluster-diagram":::

Para saber mais sobre a arquitetura, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?](big-data-cluster-overview.md).

## <a name="deployed-pods"></a>Pods implantados

A tabela a seguir lista os pods implantados em um cluster de Big Data.

|Nome  |Área|
|---------|---------|
|`control-<nnnn>`        |[Controle](#control)|
|`controldb-<#>`         |[Controle](#control)|
|`controlwd-<nnnn>`      |[Controle](#control)|
|`logsdb-<#>`            |[Controle](#control)|
|`logsui-<nnnn>`         |[Controle](#control)|
|`metricsdb-<#>`         |[Controle](#control)|
|`metricsdc-<nnnn>`      |[Controle](#control)|
|`metricsui-<nnnn>`      |[Controle](#control)|
|`mgmtproxy-<nnnn>`      |[Controle](#control)|
|`zookeeper-<#>`         |[Controle](#control)|
|`dns-<nnnn>`            |[Controle](#control)|
|`master-<#n>`           |[Instância mestra](#master-instance)|
|`operator-<nnnn>`       |[Instância mestra](#master-instance)
|`compute-<#n>-<#m>`     |[Pool de computação](#compute-pool)|
|`data-<#>-<#>`          |[Pool de dados](#data-pool) |
|`storage-<#>-<#>`       |[Pool de armazenamento](#storage-pool)|
|`nmnode-<#>-<#>`        |[Pool de armazenamento](#storage-pool)|
|`sparkhead-<#>`         |[Pool de armazenamento](#storage-pool)|
|`appproxy-<#m>`         |[Pool de aplicativos](#application-pool)|
|`gateway-<#>`           |[Serviço do gateway](#gateway-service)|

Nem todos os pods estão incluídos em todos os clusters do BDC. As implantações com alta disponibilidade ou integração de diretórios ativas incluem pods específicos. 

### <a name="high-availability-specific-pods"></a>Pods específicos de alta disponibilidade:

- `operator-<nnnn>`
- `zookeeper-<#>`

### <a name="active-directory-specific-pods"></a>Pods específicos do Active Directory:

- `dns-<nnnn>`

As seções a seguir descrevem os pods e listam os contêineres em cada pod.

## <a name="control"></a>Control

Os pods de controle fornecem o serviço de controle.

|Nome do pod |Contagem| Tipo de controlador do Kubernetes | Contêineres |
|--------|----|------|--------|-------|
|`control-#`|1| ReplicaSet |- `controller`<br><br>- `security-support`<br><br>- `fluentbit`
|`controldb`|1| StatefulSet |- `mssql-server`<br><br>- `fluentbit`
|`controlwd`|1|  ReplicaSet |- `controlwatchdog`
|`logsdb-#` |1| StatefulSet |- `elasticsearch`
|`logsui`   |1| ReplicaSet |- `kibana`
|`metricsdb-#`|1| StatefulSet |- `influxdb`
|`metricsdc`|1 por nó do Kubernetes. | DaemonSet |- `telegraf` |
|`metricsui-nnnn`|1| ReplicaSet |- `grafana` |
|`mgmtproxy-nnnn`|1| ReplicaSet |- `service-proxy`<br><br>- `fluentbit`|
|`dns-nnnn`|0 ou 1 para a integração do Active Directory| ReplicaSet |- `dns`<br><br>- `fluentbit`|

## <a name="master-instance"></a>Instância principal

`master-<#n>` é a instância mestra do SQL Server.

- Gerencia o pool de dados via DDL
- Manipula dados no pool de dados por meio de DML
- Descarrega a execução de consulta analítica no pool de dados

|Nome do pod |Contagem| Tipo de controlador do Kubernetes | Contêineres |
|--------|----|------|--------|
|`master-<#n>`|1 ou mais para alta disponibilidade.| StatefulSet|- `mssql-server`<br><br>- `fluentbit`<br><br>- `collectd`<br><br>- `mssql-ha-supervisor` <sup>*</sup>|
|`operator`<sup>*</sup>| 0 ou 1 para alta disponibilidade | ReplicaSet |- `mssql-ha-operator`

<sup>*</sup> Somente implantações de alta disponibilidade. O operador implementa e registra a definição do recurso personalizado para o SQL Server e os recursos do Grupo de Disponibilidade. Quando o operador é implantado, registra-se como ouvinte de notificações sobre os recursos do SQL Server sendo implantados no cluster do Kubernetes. `mssql-ha-supervisor` é compatível com o grupo de disponibilidade.

Cada pod `master` contém uma instância do SQL Server. Uma implantação de alta disponibilidade inclui três pods. Cada pod tem uma instância do SQL Server com bancos de dados em um Grupos de Disponibilidade Always On do SQL Server.

Inclua mais pods no tempo de implantação, de acordo com sua carga de trabalho. 

## <a name="compute-pool"></a>Pool de computação

O pool de computação fornece uma instância do SQL Server para computação.

|Nome do pod |Contagem| Tipo de controlador do Kubernetes | Contêineres |
|--------|----|------|--------|
|`compute-<#n>-<#m>`|1 ou mais.| StatefulSet |- `mssql-server`<br><br>- `fluentbit`<br><br>- `collectd`

- `#n` identifica o pool de computação.
- `#m` identifica a ID da instância no pool.

As instâncias do SQL Server para o pool de computação são sem estado. Eles só precisam de armazenamento para `tempdb`.

Inclua mais pods no tempo de implantação, de acordo com sua carga de trabalho. 

## <a name="data-pool"></a>Pool de dados

O pool de dados fornece instâncias do SQL Server para armazenamento e computação.

|Nome do pod |Contagem| Tipo de controlador do Kubernetes | Contêineres |
|--------|----|------|--------|-------|
|`data-<#n>-<#m>` | 0 ou mais | StatefulSet | -` mssql-server` <br><br>- `fluentbit`<br><br>- `collectd`|

- `#n` identifica o pool de dados.
- `#m` identifica a ID da instância no pool.

Inclua mais pods no tempo de implantação, de acordo com a carga de trabalho.

## <a name="storage-pool"></a>Pool de armazenamento

O pool de armazenamento fornece ingestão de dados por meio do Spark, armazenamento no HDFS, acesso a dados por meio do HDFS e pontos de extremidade do SQL Server.

|Nome do pod |Contagem| Tipo de controlador do Kubernetes | Contêineres |
|--------|----|------|--------|
|`storage-0-#`|1 ou mais. Inclua mais pods no tempo de implantação, de acordo com a carga de trabalho. | StatefulSet |- `hadoop`<br><br>- `mssql-server`<br><br>- `fluentbit`<br><br>
|`nmnode-0-#`|1 ou mais para alta disponibilidade| StatefulSet |- `hadoop`<br><br>- `fluentbit`
|`sparkehead-#`|1 ou mais para alta disponibilidade| StatefulSet |- `hadoop-yarn-jobhistory`<br><br>- `hadoop-livy-sparkhistory`<br><br>- `hadoop-hivemetastore`<br><br>-- `fluentbit`
|`zookeeper`|0 ou 3 para alta disponibilidade. | StatefulSet |- `zookeeper`<br><br>- `fluentbit`

## <a name="application-pool"></a>Pool de aplicativos

O pool de aplicativos está incluído em alguns dos perfis de configuração de teste. O pool de aplicativos hospeda proxies de serviço de aplicativo que você define ao implantar aplicativos em clusters de Big Data. 

`appproxy` é uma API Web que fica na frente dos aplicativos do pool de aplicativos. Ela autentica os usuários e, em seguida, roteia as solicitações até os aplicativos.

|Nome do pod | Tipo de controlador do Kubernetes | Contêineres  |
|--------|----|------|
|`appproxy`| ReplicaSet |- `app-service-proxy`<br><br>- `fluentbit`

Para saber mais, confira [O que é a Implantação de Aplicativos em um cluster de Big Data?](concept-application-deployment.md).

Inclua mais pods no tempo de implantação, de acordo com a carga de trabalho. 

## <a name="gateway-service"></a>Serviço do gateway

Os serviços de gateway fornecem o gateway do Knox para Spark, o HDFS, o [Yarn](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html), a interface do usuário do Yarn e a interface do usuário do Spark.

|Nome do pod | Tipo de controlador do Kubernetes | Contêineres |
|--------|-----|-----|
|`gateway-<#>`| StatefulSet |- `knox`<br><br>- `fluentbit`

Somente um gateway é compatível.

## <a name="open-source-container-references"></a>Referências de contêiner open-source

Alguns contêineres são desenvolvidos por projetos open-source. Para saber mais sobre os contêineres open-source usados, confira:

- [Elasticsearch](https://www.elastic.co/)
- [Kibana](https://www.elastic.co/kibana)
- [InfluxDB](https://www.influxdata.com)
- [Grafana](https://grafana.com/)
- [Fluent Bit](https://docs.fluentbit.io/manual/about/what-is-fluent-bit)
- [HDFS DataNode](concept-storage-pool.md)
- [HDFS NameNode](https://cwiki.apache.org/confluence/display/HADOOP2/NameNode) 
- [Spark](configure-spark-hdfs.md)
- [ZooKeeper](https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/) 


## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
- [Como implantar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md#configfile)
