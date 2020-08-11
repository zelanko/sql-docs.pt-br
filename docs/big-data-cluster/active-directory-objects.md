---
title: Objetos do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Saiba mais sobre a implantação de cluster de Big Data do SQL Server no Domínio do Active Directory.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e4f8736beeac2e92d25092c60c3fe7e60127ea94
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942738"
---
# <a name="auto-generated-active-directory-objects"></a>Objetos do Active Directory gerados automaticamente

Este artigo descreve quais são as contas e os grupos do AD (Active Directory) criados pelo SQL Server durante uma implantação do BDC (cluster de Big Data).

## <a name="accounts--groups"></a>Contas e grupos

As contas e os grupos de usuário são gerados na [UO (unidade organizacional)](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts) fornecida durante a implantação do cluster.

Cada uma das contas representa um serviço no BDC. As contas são proprietárias dos SPNs (nomes da entidade de serviço) necessários para cada serviço. Os SPNs de propriedade de cada conta podem ser listados com o comando [setspn](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spn-setspn-syntax.aspx).

A implantação gera automaticamente nomes de contas e grupos. Do SQL Server 2019 CU5 em diante, o prefixo de nome da conta ou do grupo é o nome do namespace de implantação (nome do cluster BDC). Se o nome do cluster for `bdc` para os itens neste artigo, substitua `<prefix>` por `bdc` para identificar suas contas.

O sufixo do pod (-x) indica uma ID de pod variável abaixo. Os nomes abaixo não incluem um prefixo de variável que é fornecido pelo usuário durante a implantação.

O nome da conta clássica se aplica às implantações que usam versões anteriores ao SQL Server 2019 CU5, bem como às implantações feitas com a opção "useSubdomain" definida como falso na configuração de segurança.

| Nome da conta ou do grupo|Mais informações|
|----|---|
|`<prefix>-ctrl`|[Conta de serviço do controlador](#controller-service-account)|
|`<prefix>-ngxm`|[Conta de serviço do proxy de serviço de monitoramento](#monitoring-service-proxy-service-account)|
|`<prefix>-ldap`|[Usuário de pesquisa LDAP](#ldap-lookup-user)|
|`<prefix>-sqc0-x/<prefix>-sqc0`|[Usuário do SQL Server do pool de computação](#compute-pool-sql-server-user)|
|`<prefix>-dmc0-x`|[Usuário do DMS do Data Warehouse do pool de computação](#compute-pool-data-warehouse-dms-user)|
|`<prefix>-dec0-x`|[Usuário do Mecanismo de Data Warehouse do pool de computação](#compute-pool-data-warehouse-engine-user)|
|`<prefix>-sqd0`|[Usuário do SQL Server do pool de dados](#data-pool-sql-server-user)|
|`<prefix>-sqs0`|[Usuário do SQL Server do pool de armazenamento](#storage-pool-sql-server-user)|
|`<prefix>-ynt0-x`|[Usuário do serviço do gerenciador de nós do Yarn do pool de armazenamento](#storage-pool-yarn-node-manager-service-user)|
|`<prefix>-htt0`|[Usuário do serviço HTTP do pool de armazenamento](#storage-pool-http-service-user)|
|`<prefix>-hdt0`|[Usuário do serviço de datanode do HDFS do pool de armazenamento](#storage-pool-hdfs-datanode-service-user)|
|`<prefix>-hdnn`|[Usuário do serviço de nó de nome do HDFS](#hdfs-name-node-service-user)|
|`<prefix>-htnn`|[Usuário do serviço HTTP do nó de nome do HDFS](#hdfs-name-node-http-service-user)|
|`<prefix>-kmnn-x`|[Usuário do serviço KMS do nó de nome](#name-node-kms-service-user)|
|`<prefix>-jnzk-x`|[Usuários do serviço JournalNode do ZooKeeper](#zookeeper-journalnode-service-users)|
|`<prefix>-htzk`|[Usuário do serviço HTTP do ZooKeeper](#zookeeper-http-service-user)|
|`<prefix>-yrsh-x`|[Usuário do serviço de gerenciador de recursos do Yarn do Sparkhead](#sparkhead-yarn-resource-manager-service-user)|
|`<prefix>-htsh`|[Usuário HTTP do Sparkhead](#sparkhead-http-user)|
|`<prefix>-shsh-x`|[Usuário do serviço de histórico do Spark do Sparkhead](#sparkhead-spark-history-service-user)|
|`<prefix>-lvsh-x`|[Usuário do serviço do Livy do Sparkhead](#sparkhead-livy-service-user)|
|`<prefix>-hvsh-x`|[Usuário do serviço do Hive do Sparkhead](#sparkhead-hive-service-user)|
|`<prefix>-yns0-x`|[Usuário do serviço de gerenciador de nós do Yarn do Pool do Spark](#spark-pool-yarn-node-manager-service-user)|
|`<prefix>-hts0`|[Usuário HTTP do gerenciador de nós do Yarn do Pool do Spark](#spark-pool-yarn-node-manager-http-user)|
|`<prefix>-knox-x`|[Usuário do Gateway do Knox](#knox-gateway-user)|
|`<prefix>-htgw`|[Usuário HTTP do Gateway do Knox](#knox-gateway-http-user)|
|`<prefix>-apst`|[Usuário de instalação do aplicativo](#app-setup-user)|
|`<prefix>-dmsvc`|[Grupo do serviço DMS do Data Warehouse](#data-warehouse-dms-service-group)|
|`<prefix>-desvc`|[Grupo do serviço do Mecanismo de Data Warehouse](#data-warehouse-engine-service-group)|

A seção a seguir fornece mais detalhes sobre cada conta. Para obter informações sobre grupos, vá para [Grupos](#groups).

## <a name="controller-management--ldap-related-accounts"></a>Controlador, gerenciamento e contas relacionadas ao LDAP

### <a name="controller-service-account"></a>Conta de serviço do controlador

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`control`|
|Nome do pod|`control-x`|
|Nome do contêiner|`controller`|
|Nome do serviço|`controller`|
|Nome da conta (sem prefixo)| `ctrl`|
|Conta (com prefixo de namespace)|`<prefix>-ctrl`|
|Nome da conta clássica|`ctrl-controller`|

### <a name="monitoring-service-proxy-service-account"></a>Conta de serviço do proxy de serviço de monitoramento

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`mgmtproxy`|
|Nome do pod|`mgmtproxy-x`|
|Nome do contêiner|`service-proxy`|
|Nome do serviço|`nginx`|
|Conta (sem prefixo)| `ngxm`|
|Conta (com prefixo de namespace)|`<prefix>-ngxm`|
|Nome da conta clássica|`nginx-mgmtproxy`|

### <a name="ldap-lookup-user"></a>Usuário de pesquisa LDAP

Usado pelos serviços Grafana e Hadoop para pesquisar usuários por meio do LDAP.

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`metricsui`|
|Nome do pod|`metricsui-x`|
|Nome do contêiner|`grafana`|
|Nome do serviço|`grafana`|
|Nome da conta (sem prefixo)| `ldap`|
|Nome da conta (com o prefixo do namespace)|`<prefix>-ldap`|
|Nome da conta clássica|`ldap-user`|

## <a name="master-pool-accounts"></a>Contas do pool mestre

### <a name="master-pool-sql-server-user"></a>Usuário do SQL Server do pool mestre

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`master`|
|Nome do pod|`master-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`mssql`|
|Nome da conta (sem prefixo)| `sqmp-x/sqmp`|
|Nome da conta (com o prefixo do namespace)|`<prefix>-sqmp-x/<prefix>-sqmp`|
|Nome da conta clássica|`mssql-master-x`|

### <a name="master-pool-data-warehouse-dms-user"></a>Usuário do DMS do Data Warehouse do pool mestre

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`master`|
|Nome do pod|`master-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`dwdms`|
|Conta (sem prefixo)| `dmmp-x`|
|Conta (com prefixo de namespace)|`<prefix>-dmmp-x`|
|Nome da conta clássica|`dwdms-master-x`|

### <a name="master-pool-data-warehouse-engine-user"></a>Usuário do Mecanismo de Data Warehouse do pool mestre

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`master`|
|Nome do pod|`master-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`dweng`|
|Conta (sem prefixo)| `demp`|
|Conta (com prefixo de namespace)|`<prefix>-demp-x`|
|Nome da conta clássica|`dweng-master-x`|

## <a name="compute-pool-accounts"></a>Contas do pool de computação

### <a name="compute-pool-sql-server-user"></a>Usuário do SQL Server do pool de computação

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`compute-0`|
|Nome do pod|`compute-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`mssql`|
|Conta (sem prefixo)| `sqc0-x/sqlc0`|
|Conta (com prefixo de namespace)|`<prefix>-sqc0-x/<prefix>-sqc0`|
|Nome da conta clássica|`mssql-compute-0-x`|

### <a name="compute-pool-data-warehouse-dms-user"></a>Usuário do DMS do Data Warehouse do pool de computação

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`compute-0`|
|Nome do pod|`compute-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`dwdms`|
|Conta (sem prefixo)| `dmc0-x`|
|Conta (com prefixo de namespace)|`<prefix>-dmc0-x`|
|Nome da conta clássica|`dwdms-compute-0-x`|

### <a name="compute-pool-data-warehouse-engine-user"></a>Usuário do Mecanismo de Data Warehouse do pool de computação

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`compute-0`|
|Nome do pod|`compute-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`dweng`|
|Conta (sem prefixo)| `dec0-x`|
|Conta (com prefixo de namespace)|`<prefix>-dec0-x`|
|Nome da conta clássica|`dweng-compute-0-x`|

## <a name="data-pool-accounts"></a>Contas do pool de dados

### <a name="data-pool-sql-server-user"></a>Usuário do SQL Server do pool de dados

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`data-0`|
|Nome do pod|`data-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`mssql`|
|Conta (sem prefixo)| `sqd0`|
|Conta (com prefixo de namespace)|`<prefix>-sqd0`|
|Nome da conta clássica|`mssql-data-0`|

## <a name="storage-pool-accounts"></a>Contas do pool de armazenamento

### <a name="storage-pool-sql-server-user"></a>Usuário do SQL Server do pool de armazenamento

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`storage-0`|
|Nome do pod|`storage-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`mssql`|
|Conta (sem prefixo)| `sqs0`|
|Conta (com prefixo de namespace)|`<prefix>-sqs0`|
|Nome da conta clássica|`mssql-storage-0`|

### <a name="storage-pool-yarn-node-manager-service-user"></a>Usuário do serviço do gerenciador de nós do Yarn do pool de armazenamento

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`storage-0`|
|Nome do pod|`storage-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`Yarn Node Manager`|
|Conta (sem prefixo)| `ynt0-x`|
|Conta (com prefixo de namespace)|`<prefix>-ynt0-x`|
|Nome da conta clássica|`yarnnm-storage-0-x`|

### <a name="storage-pool-http-service-user"></a>Usuário do serviço HTTP do pool de armazenamento

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`storage-0`|
|Nome do pod|`storage-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`HDFS Datanode`|
|Conta (sem prefixo)| `hdt0`|
|Conta (com prefixo de namespace)|`<prefix>-hdt0`|
|Nome da conta clássica|`http-storage-0`|

### <a name="storage-pool-hdfs-datanode-service-user"></a>Usuário do serviço de datanode do HDFS do pool de armazenamento

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`storage-0`|
|Nome do pod|`storage-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`HDFS Datanode`|
|Conta (sem prefixo)| `hdt0`|
|Conta (com prefixo de namespace)|`<prefix>-hdt0`|
|Nome da conta clássica|`hdfsdn-storage-0`|

## <a name="hdfs-accounts"></a>Contas do HDFS

### <a name="hdfs-name-node-service-user"></a>Usuário do serviço de nó de nome do HDFS

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`nmnode-0`|
|Nome do pod|`nmnode-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`HDFS Namenode`|
|Conta (sem prefixo)| `hdnn`|
|Conta (com prefixo de namespace)|`<prefix>-hdnn`|
|Nome da conta clássica|`hdfsnn-nmnode`|

### <a name="hdfs-name-node-http-service-user"></a>Usuário do serviço HTTP do nó de nome do HDFS

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`nmnode-0`|
|Nome do pod|`nmnode-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`HDFS Namenode`|
|Conta (sem prefixo)| `htnn`|
|Conta (com prefixo de namespace)|`<prefix>-htnn`|
|Nome da conta clássica|`http-nmnode`|

## <a name="kms-accounts"></a>Contas do KMS

### <a name="name-node-kms-service-user"></a>Usuário do serviço KMS do nó de nome

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`nmnode-0`|
|Nome do pod|`nmnode-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`KMS`|
|Conta (sem prefixo)| `kmnn-x`|
|Conta (com prefixo de namespace)|`<prefix>-kmnn-x`|
|Nome da conta clássica|`kms-nmnode-x`|

## <a name="zookeeper-accounts"></a>Contas do ZooKeeper

### <a name="zookeeper-journalnode-service-users"></a>Usuários do serviço JournalNode do ZooKeeper

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`zookeeper`|
|Nome do pod|`zookeeper-x`|
|Nome do contêiner|`zookeeper`|
|Nome do serviço|`Journal node`|
|Conta (sem prefixo)| `jnzk-x`|
|Conta (com prefixo de namespace)|`<prefix>-jnzk-x`|
|Nome da conta clássica|`jn-zookeeper-x`|

### <a name="zookeeper-http-service-user"></a>Usuário do serviço HTTP do ZooKeeper

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`zookeeper`|
|Nome do pod|`zookeeper-x`|
|Nome do contêiner|`zookeeper`|
|Nome do serviço|`Zookeeper`|
|Conta (sem prefixo)| `htzk`|
|Conta (com prefixo de namespace)|`<prefix>-htzk`|
|Nome da conta clássica|`http-zookeeper`|

## <a name="spark-related-accounts"></a>Contas relacionadas ao Spark

### <a name="sparkhead-yarn-resource-manager-service-user"></a>Usuário do serviço de gerenciador de recursos do Yarn do Sparkhead

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`sparkhead`|
|Nome do pod|`sparkhead-x`|
|Nome do contêiner|`hadoop-yarn-jobhistory`|
|Nome do serviço|`Yarn Resource Manager`|
|Conta (sem prefixo)| `yrsh-x`|
|Conta (com prefixo de namespace)|`<prefix>-yrsh-x`|
|Nome da conta clássica|`yarnrm-sparkhead-x`|

### <a name="sparkhead-http-user"></a>Usuário HTTP do Sparkhead

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`sparkhead`|
|Nome do pod|`sparkhead-x`|
|Nome do contêiner|`*`|
|Nome do serviço|`*`|
|Conta (sem prefixo)| `htsh`|
|Conta (com prefixo de namespace)|`<prefix>-htsh`|
|Nome da conta clássica|`http-sparkhead`|

### <a name="sparkhead-spark-history-service-user"></a>Usuário do serviço de histórico do Spark do Sparkhead

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`sparkhead`|
|Nome do pod|`sparkhead-x`|
|Nome do contêiner|`hadoop-livy-sparkhistory`|
|Nome do serviço|`Spark History Server`|
|Conta (sem prefixo)| `shsh-x`|
|Conta (com prefixo de namespace)|`<prefix>-shsh-x`|
|Nome da conta clássica|`sph-sparkhead-x`|

### <a name="sparkhead-livy-service-user"></a>Usuário do serviço do Livy do Sparkhead

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`sparkhead`|
|Nome do pod|`sparkhead-x`|
|Nome do contêiner|`hadoop-livy-sparkhistory`|
|Nome do serviço|`Livy`|
|Conta (sem prefixo)| `lvsh-x`|
|Conta (com prefixo de namespace)|`<prefix>-lvsh-x`|
|Nome da conta clássica|`livy-sparkhead-x`|

### <a name="sparkhead-hive-service-user"></a>Usuário do serviço do Hive do Sparkhead

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`sparkhead`|
|Nome do pod|`sparkhead-x`|
|Nome do contêiner|`hadoop-hivemetastore`|
|Nome do serviço|`Hive Metastore`|
|Conta (sem prefixo)| `hvsh-x`|
|Conta (com prefixo de namespace)|`<prefix>-hvsh-x`|
|Nome da conta clássica|`hive-sparkhead-x`|

### <a name="spark-pool-yarn-node-manager-service-user"></a>Usuário do serviço de gerenciador de nós do Yarn do Pool do Spark

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`spark-0`|
|Nome do pod|`spark-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`Yarn Node Manager`|
|Conta (sem prefixo)| `yns0-x`|
|Conta (com prefixo de namespace)|`<prefix>-yns0-x`|
|Nome da conta clássica|`yarnnm-spark-0-x`|

### <a name="spark-pool-yarn-node-manager-http-user"></a>Usuário HTTP do gerenciador de nós do Yarn do Pool do Spark

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`spark-0`|
|Nome do pod|`spark-0-x`|
|Nome do contêiner|`hadoop`|
|Nome do serviço|`Yarn Node Manager`|
|Conta (sem prefixo)| `hts0`|
|Conta (com prefixo de namespace)|`<prefix>-hts0`|
|Nome da conta clássica|`http-spark-0`|

## <a name="knox-accounts"></a>Contas do Knox

### <a name="knox-gateway-user"></a>Usuário do Gateway do Knox

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`gateway`|
|Nome do pod|`gateway-x`|
|Nome do contêiner|`knox`|
|Nome do serviço|`Knox`|
|Conta (sem prefixo)| `knox-x`|
|Conta (com prefixo de namespace)|`<prefix>-knox-x`|
|Nome da conta clássica|`knox-gateway-x`|

### <a name="knox-gateway-http-user"></a>Usuário HTTP do Gateway do Knox

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`gateway`|
|Nome do pod|`gateway-x`|
|Nome do contêiner|`knox`|
|Nome do serviço|`Knox`|
|Conta (sem prefixo)| `htgw`|
|Conta (com prefixo de namespace)|`<prefix>-htgw`|
|Nome da conta clássica|`http-gateway`|

## <a name="app-accounts"></a>Contas de aplicativos

### <a name="app-setup-user"></a>Usuário de instalação do aplicativo

|Objeto|Nome da conta|
|---|---|
|Nome do conjunto de dimensionamento|`appproxy`|
|Nome do pod|`appproxy-x`|
|Nome do contêiner|`App Service Proxy`|
|Nome do serviço|`nginx`|
|Conta (sem prefixo)| `apst`|
|Conta (com prefixo de namespace)|`<prefix>-apst`|
|Nome da conta clássica|`app-setup`|

## <a name="groups"></a>Grupos

Os grupos a seguir são criados na UO fornecida pelo usuário. Os membros dos grupos são os usuários criados acima para os serviços correspondentes.

### <a name="data-warehouse-dms-service-group"></a>Grupo do serviço DMS do Data Warehouse

|Objeto|Nome do grupo|
|---|---|
|Nome do conjunto de dimensionamento|`master/compute-0`|
|Nome do pod|`master-x/compute-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`dwdms`|
|Grupo (sem prefixo)| `dmsvc`|
|Conta (com prefixo de namespace)|`<prefix>-dmsvc`|
|Nome da conta clássica|`dwdms-service`|

### <a name="data-warehouse-engine-service-group"></a>Grupo do serviço do Mecanismo de Data Warehouse

|Objeto|Nome do grupo|
|---|---|
|Nome do conjunto de dimensionamento|`master/compute-0`|
|Nome do pod|`master-x/compute-0-x`|
|Nome do contêiner|`mssql-server`|
|Nome do serviço|`dweng`|
|Grupo (sem prefixo)| `desvc`|
|Conta (com prefixo de namespace)|`<prefix>-desvc`|
|Nome da conta clássica|`desvc`|

## <a name="next-steps"></a>Próximas etapas

[Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](deploy-active-directory.md)

[Implantar vários [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no mesmo domínio do Active Directory](active-directory-deployment-background.md)
