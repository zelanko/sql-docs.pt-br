---
title: Monitorar a replicação de forma programática | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_replmonitorhelppublisher
- sp_replmonitorhelpmergesessiondetail
- monitoring performance [SQL Server replication], publication status
- sp_replmonitorhelpmergesession
- sp_replmonitorhelppublicationthresholds
- monitoring performance [SQL Server replication], subscription status
- monitoring performance [SQL Server replication], Transact-SQL programming
- sp_replmonitorsubscriptionpendingcmds
- sp_replmonitorchangepublicationthreshold
- transactional replication, monitoring
- sp_replmonitorhelppublication
- sp_replmonitorhelpsubscription
- monitoring performance [SQL Server replication], thresholds and warnings
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0926264c25affe2f110227fad4c0fb2b113c9590
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287850"
---
# <a name="programmatically-monitor-replication"></a>Monitore programaticamente a replicação
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  O Replication Monitor é uma ferramenta gráfica que permite monitorar uma topologia de replicação. É possível acessar os mesmos dados de monitoração programaticamente usando o RMO (Replication Management Objects) ou procedimentos armazenados de replicação do [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Esses objetos permitem programar as seguintes tarefas:  
  
-   Monitorar o estado de Publicadores, publicações e assinaturas.  
  
-   Monitorar as sessões do Merge Agent em um ou mais Assinantes.  
  
-   Monitorar os comandos transacionais que estão esperando para serem aplicados em um ou mais Assinantes.  
  
-   Definir os limites métricos que determinam quando uma publicação requer intervenção.  
  
-   Monitorar o estado de tokens de rastreamento.  
  
 **Neste tópico:**  
  
 [Transact-SQL](#Tsql)  
  
 [RMO (Replication Management Objects)](#RMO)  
  
##  <a name="transact-sql"></a><a name="Tsql"></a> Transact-SQL  
  
#### <a name="to-monitor-publishers-publications-and-subscriptions-from-the-distributor"></a>Para monitorar Publicador, publicações e assinatura a partir do Distribuidor  
  
1.  No Distribuidor, no banco de dados de distribuição, execute [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md). Isso retornará informações para todos os Publicadores que usarem esse Distribuidor. Para limitar o conjunto de resultados a um único Publicador, especifique **\@publisher**.  
  
2.  No Distribuidor do banco de dados de distribuição, execute [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md). Isso retornará informações para todas as publicações que usarem esse Distribuidor. Para limitar o conjunto de resultados a um único Publicador, publicação ou banco de dados publicado, especifique **\@publisher**, **\@publication** ou **\@publisher_db**, respectivamente.  
  
3.  No Distribuidor do banco de dados de distribuição, execute [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md). Isso retornará informações para todas as assinaturas que usarem esse Distribuidor. Para limitar o conjunto de resultados às assinaturas pertencentes a um único Publicador, publicação ou banco de dados publicado, especifique **\@publisher**, **\@publication** ou **\@publisher_db**, respectivamente.  
  
#### <a name="to-monitor-transactional-commands-waiting-to-be-applied-at-the-subscriber"></a>Para monitorar os comandos transacionais que estão esperando para serem aplicados no Assinante.  
  
1.  No Distribuidor do banco de dados de distribuição, execute [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md). Isso retornará informações de monitoração para todos os comandos pendentes, de todas as assinaturas que usam esse Distribuidor. Para limitar o conjunto de resultados aos comandos pendentes das assinaturas pertencentes a um único Publicador, publicação ou banco de dados publicado, especifique **\@publisher**, **\@subscriber**, **\@publication** ou **\@publisher_db**, respectivamente.  
  
#### <a name="to-monitor-merge-changes-waiting-to-be-uploaded-or-downloaded"></a>Para monitorar as alterações de mesclagem a espera de serem carregadas ou baixadas  
  
1.  No Publicador do banco de dados de publicação, execute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). Isso retornará um conjunto de resultados que mostra informações sobre as alterações esperando para ser replicadas nos Assinantes. Para limitar o conjunto de resultados às mudanças pertencentes a um único Publicador, publicação ou artigo, especifique **\@publication** ou **\@article**, respectivamente.  
  
2.  Em um Assinante, no banco de dados da assinatura, execute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). Isso retornará um conjunto de resultados que mostra informações sobre as alterações esperando para ser replicadas no Publicador. Para limitar o conjunto de resultados às mudanças pertencentes a um único Publicador, publicação ou artigo, especifique **\@publication** ou **\@article**, respectivamente.  
  
#### <a name="to-monitor-merge-agent-sessions"></a>Para monitorar sessões do Merge Agent  
  
1.  No Distribuidor do banco de dados de distribuição, execute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Isso retornará informações de monitoração, inclusive **Session_id**, em todas as sessões do Merge Agent de todas as assinaturas que usam esse Distribuidor. Você também pode obter o **Session_id** consultando a tabela do sistema [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) .  
  
2.  No Distribuidor, no banco de dados de distribuição, execute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique um valor de **Session_id** da etapa 1 para **\@session_id**. Isso exibirá informações de monitoramento detalhadas sobre a sessão.  
  
3.  Repita a etapa 2 para cada sessão que interessar.  
  
#### <a name="to-monitor-merge-agent-sessions-for-pull-subscriptions-from-the-subscriber"></a>Para monitorar sessões do Merge Agent para assinatura pull do Assinante  
  
1.  No Assinante, no banco de dados da assinatura, execute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Para uma assinatura determinada, especifique **\@publisher**, **\@publication** e o nome do banco de dados de publicação para **\@publisher_db**. Isso retornará informações de monitoração das últimas cinco sessões do Merge Agent para essa assinatura. Observe que o valor de **Session_id** para as sessões que interessarem, no conjunto de resultados.  
  
2.  No Assinante, no banco de dados da assinatura, execute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique um valor de **Session_id** da etapa 1 para **\@session_id**. Isso exibirá informações de monitoramento detalhadas sobre a sessão.  
  
3.  Repita a etapa 2 para cada sessão que interessar.  
  
#### <a name="to-view-and-modify-the-monitor-threshold-metrics-for-a-publication"></a>Para exibir e modificar as métricas de limite do monitor para uma publicação  
  
1.  No Distribuidor, no banco de dados de distribuição, execute [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md). Isso retornará o conjunto de limites de monitoramento, para todas as publicações que usam esse Distribuidor. Para limitar o conjunto de resultados e monitorar os limites das publicações pertencentes a um único Publicador, a um banco de dados publicado ou a uma única publicação, especifique **\@publisher**, **\@publisher_db** ou **\@publication**, respectivamente. Observe o valor de **Metric_id** para qualquer limite que deva ser alterado. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  No Distribuidor, no banco de dados de distribuição, execute [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md). Especifique o seguinte, quando necessário:  
  
    -   O valor **Metric_id** obtido na etapa 1 para **\@metric_id**.  
  
    -   Um valor novo para a métrica de limite do monitor para **\@value**.  
  
    -   O valor **1** para **\@shouldalert**, para ser registrado um alerta, quando esse limite for atingido, ou o valor **0**, se não for necessário um alerta.  
  
    -   Um valor **1** para **\@mode**, para habilitar a métrica de limite do monitor, ou um valor **2** para desabilitá-la.  
  
##  <a name="replication-management-objects-rmo"></a><a name="RMO"></a> RMO (Replication Management Objects)  
  
#### <a name="to-monitor-a-subscription-to-a-merge-publication-at-the-subscriber"></a>Para monitorar uma assinatura para uma publicação de mesclagem no Assinante  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> e defina as propriedades <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> para a assinatura, e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
3.  Chame um dos métodos seguintes para retornar informações sobre as sessões do Merge Agent para essa assinatura:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> - retorna uma matriz de objetos <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> com informações até as últimas cinco sessões do Merge Agent. Observe o valor <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> para qualquer sessão do seu interesse.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> - retorna uma matriz de objetos <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> com informações das sessões do Merge Agent que ocorreram durante o número de horas passadas no parâmetro *hours* (até as últimas cinco sessões). Observe o valor <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> para qualquer sessão do seu interesse.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> - retorna um objeto <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> com informações sobre a última sessão do Merge Agent. Observe o valor de <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> para esta sessão.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> - retorna uma matriz de objetos <xref:System.Data.DataSet> com informações até as últimas cinco sessões do Merge Agent, uma em cada linha. Observe o valor da coluna **Session_id** para qualquer sessão do seu interesse.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> - retorna um objeto <xref:System.Data.DataRow> com informações sobre a última sessão do Merge Agent. Observe o valor da coluna **Session_id** para essa sessão.  
  
4.  (Opcional) Chame o <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> para atualizar os dados para o objeto <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> passado como *mss,* ou chame <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> para atualizar os dados no objeto <xref:System.Data.DataRow> passado como *drRefresh*.  
  
5.  Usando a id de sessão obtida na etapa 3, chame um dos métodos seguintes para retornar informações sobre os detalhes de uma sessão em particular:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> - retorna uma matriz de objetos <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> para a *SessionId*.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> - retorna um objeto <xref:System.Data.DataSet> com informações para a *SessionId*.  
  
#### <a name="to-monitor-replication-properties-for-all-publications-at-a-distributor"></a>Para monitorar as propriedades de replicação para todas as publicações em um Distribuidor  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationMonitor>.  
  
3.  Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criada na etapa 1.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
5.  Execute um ou mais dos métodos seguintes para retornar informações de replicação para todos os Publicador que usam esse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os Distribution Agents nesse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre os erros armazenados no Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os Log Reader Agents no Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os Merge Agents no Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os outros agentes de replicação no Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os Publicador nesse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> - retorna um objeto <xref:System.Data.DataSet> que retorna os Publicadores que usam esse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os Queue Reader Agents no Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> - retorna um objeto <xref:System.Data.DataSet> que contém detalhes sobre o Queue Reader Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações de sessão sobre o Queue Reader Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os Snapshot Agents no Distribuidor.  
  
#### <a name="to-monitor-publication-properties-for-a-specific-publisher-at-the-distributor"></a>Para monitorar as propriedades de publicação para um Publicador específico no Distribuidor  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Consiga um objeto <xref:Microsoft.SqlServer.Replication.PublisherMonitor> em um desses modos.  
  
    -   Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.PublisherMonitor>. Defina a propriedade <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> para o Publicador e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criada na etapa 1. Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, o nome do Publicador estava definido incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> acessado por meio da propriedade <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> de um objeto existente <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> .  
  
3.  Execute um ou mais dos métodos a seguir para retornar informações de replicação para todas as publicações que pertençam a esse Publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> - retorna um objeto <xref:System.Data.DataSet> que contém detalhes sobre o Distribution Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informação da sessão sobre o Distribution Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações de registro de erros sobre o erro especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> - retorna um objeto <xref:System.Data.DataSet> que contém detalhes sobre o Log Reader Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações de sessão sobre o Log Reader Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> - retorna um objeto <xref:System.Data.DataSet> que contém detalhes sobre o Merge Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> - retorna um objeto <xref:System.Data.DataSet> que contém detalhes adicionais sobre o Merge Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informação da sessão para o Merge Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações de sessão adicional para o Merge Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todas as publicações nesse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações adicionais sobre todas as publicações nesse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> - retorna um objeto <xref:System.Data.DataSet> que contém detalhes sobre o Snapshot Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informação da sessão para o Snapshot Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todas as assinaturas para publicações nesse Distribuidor.  
  
#### <a name="to-monitor-properties-for-a-specific-publication-at-the-distributor"></a>Para monitorar as propriedades para uma publicação específica no Distribuidor  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Consiga um objeto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> em um desses modos.  
  
    -   Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>. Defina as propriedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> para a publicação e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação foram definidas incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> acessado por meio da propriedade <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> de um objeto existente <xref:Microsoft.SqlServer.Replication.PublisherMonitor> .  
  
3.  Execute um ou mais dos métodos seguintes para retornar informações sobre essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> - retorna um objeto <xref:System.Data.DataSet> que contém registros de erro sobre o erro especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre o Log Reader Agent para essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre o conjunto de limites de monitoração de avisos para essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre o Queue Reader Agent usado por essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre o Snapshot Agent para essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre assinaturas para essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações adicionais sobre assinaturas para essa publicação com base no <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>fornecido.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações de latência para o token de rastreamento especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> - retorna um objeto <xref:System.Data.DataSet> que contém informações sobre todos os tokens de rastreamento inseridos nessa publicação.  
  
#### <a name="to-monitor-transactional-commands-that-are-waiting-to-be-applied-at-the-subscriber"></a>Para monitorar os comandos transacionais que estão esperando para serem aplicados no Assinante.  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Consiga um objeto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> em um desses modos.  
  
    -   Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>. Defina as propriedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> para a publicação e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação foram definidas incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> acessado por meio da propriedade <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> de um objeto existente <xref:Microsoft.SqlServer.Replication.PublisherMonitor> .  
  
3.  Execute o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> que retorna um objeto <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> .  
  
4.  Use as propriedades desse objeto <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> para determinar o número estimado de comandos pendentes e o tempo que levará para completar a entrega desses comandos.  
  
#### <a name="to-set-the-monitor-warning-thresholds-for-a-publication"></a>Para definir os limites de aviso de monitoração para uma publicação  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Consiga um objeto <xref:Microsoft.SqlServer.Replication.PublicationMonitor> em um desses modos.  
  
    -   Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.PublicationMonitor>. Defina as propriedades <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> para a publicação e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> como <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação foram definidas incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> acessado por meio da propriedade <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> de um objeto existente <xref:Microsoft.SqlServer.Replication.PublisherMonitor> .  
  
3.  Execute o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> . Observe as configurações de limite atuais no <xref:System.Collections.ArrayList> retornado de objetos <xref:Microsoft.SqlServer.Replication.MonitorThreshold> .  
  
4.  Execute o método <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> . Passe os seguintes parâmetros:  
  
    -   *metricID* - um valor <xref:System.Int32> que representa a métrica de limite de monitoração da tabela a seguir:  
  
        |Valor|DESCRIÇÃO|  
        |-----------|-----------------|  
        |1|**expiration** - monitora a expiração iminente de assinaturas para publicações transacionais.|  
        |2|**latency** - monitora o desempenho de assinaturas para publicações transacionais.|  
        |4|**mergeexpiration** - monitora a expiração iminente de assinaturas para publicações de mesclagem.|  
        |5|**mergeslowrunduration** - monitora a duração de sincronizações de mesclagem em conexões da baixa largura da banda (discadas).|  
        |6|**mergefastrunduration** - monitora a duração de sincronizações de mesclagem em conexões da alta largura da banda (LAN).|  
        |7|**mergefastrunspeed** - monitora a taxa de sincronizações de mesclagem em conexões de alta largura da banda (LAN).|  
        |8|**mergeslowrunspeed** - monitora a taxa de sincronizações de mesclagem em conexões de baixa largura da banda (discadas).|  
  
    -   *enable* - <xref:System.Boolean> valor que indica se a métrico está habilitado para a publicação.  
  
    -   *thresholdValue* - valor inteiro que define o limite.  
  
    -   *shouldAlert* - inteiro que indica se esse limite deve gerar um alerta.  
  
  
