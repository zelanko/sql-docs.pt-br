---
title: "Monitore programaticamente a replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
  - "sp_replmonitorhelpmergesessiondetail"
  - "monitoring performance [SQL Server replication], publication status"
  - "sp_replmonitorhelpmergesession"
  - "sp_replmonitorhelppublicationthresholds"
  - "monitoring performance [SQL Server replication], subscription status"
  - "monitoring performance [SQL Server replication], Transact-SQL programming"
  - "sp_replmonitorsubscriptionpendingcmds"
  - "sp_replmonitorchangepublicationthreshold"
  - "transactional replication, monitoring"
  - "sp_replmonitorhelppublication"
  - "sp_replmonitorhelpsubscription"
  - "monitoring performance [SQL Server replication], thresholds and warnings"
  - "merge replication monitoring [SQL Server replication]"
  - "replicação de instantâneo [SQL Server], monitorando"
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Monitore programaticamente a replica&#231;&#227;o
  O Replication Monitor é uma ferramenta gráfica que permite monitorar uma topologia de replicação. É possível acessar os mesmos dados de monitoração programaticamente usando o RMO (Replication Management Objects) ou procedimentos armazenados de replicação do [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Esses objetos permitem programar as seguintes tarefas:  
  
-   Monitorar o estado de Publicadores, publicações e assinaturas.  
  
-   Monitorar as sessões do Merge Agent em um ou mais Assinantes.  
  
-   Monitorar os comandos transacionais que estão esperando para serem aplicados em um ou mais Assinantes.  
  
-   Definir os limites métricos que determinam quando uma publicação requer intervenção.  
  
-   Monitorar o estado de tokens de rastreamento.  
  
 **Neste tópico:**  
  
 [Transact-SQL](#Tsql)  
  
 [RMO (Replication Management Objects)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### Para monitorar Publicador, publicações e assinatura a partir do Distribuidor  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md). Isso retornará informações para todos os Publicadores que usarem esse Distribuidor. Para limitar o conjunto de resultados a um único Publicador, especifique **@publisher**.  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md). Isso retornará informações para todas as publicações que usarem esse Distribuidor. Para limitar o conjunto de resultados para um único publicador, publicação ou banco de dados publicado, especifique **@publisher**, **@publication**, ou **@publisher_db**, respectivamente.  
  
3.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md). Isso retornará informações para todas as assinaturas que usarem esse Distribuidor. Para limitar o conjunto de resultados para assinaturas pertencentes a um único publicador, publicação ou banco de dados publicado, especifique **@publisher**, **@publication**, ou **@publisher_db**, respectivamente.  
  
#### Para monitorar os comandos transacionais que estão esperando para serem aplicados no Assinante.  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md). Isso retornará informações de monitoração para todos os comandos pendentes, de todas as assinaturas que usam esse Distribuidor. Para limitar o conjunto de resultados para comandos pendentes das assinaturas pertencentes a um único publicador, assinante, publicação ou banco de dados publicado, especifique **@publisher**, **@subscriber**, **@publication**, ou **@publisher_db**, respectivamente.  
  
#### Para monitorar as alterações de mesclagem a espera de serem carregadas ou baixadas  
  
1.  No publicador do banco de dados de publicação, execute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). Isso retornará um conjunto de resultados que mostra informações sobre as alterações esperando para ser replicadas nos Assinantes. Para limitar o conjunto de resultados às mudanças pertencentes a um único Publicador, publicação ou artigo, especifique **@publication** ou **@article**, respectivamente.  
  
2.  Em um assinante no banco de dados de assinatura, execute [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md). Isso retornará um conjunto de resultados que mostra informações sobre as alterações esperando para ser replicadas no Publicador. Para limitar o conjunto de resultados às mudanças pertencentes a um único Publicador, publicação ou artigo, especifique **@publication** ou **@article**, respectivamente.  
  
#### Para monitorar sessões do Merge Agent  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Isso retorna informações de monitoramento, incluindo **Session_id**, em todas as sessões do Merge Agent para todas as assinaturas que usam esse distribuidor. Você também pode obter **Session_id** consultando o [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) tabela do sistema.  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique um **Session_id** valor da etapa 1 para **@session_id**. Isso exibirá informações de monitoramento detalhadas sobre a sessão.  
  
3.  Repita a etapa 2 para cada sessão que interessar.  
  
#### Para monitorar sessões do Merge Agent para assinatura pull do Assinante  
  
1.  No assinante no banco de dados de assinatura, execute [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md). Para uma determinada assinatura, especifique **@publisher**, **@publication**, e o nome do banco de dados de publicação para **@publisher_db**. Isso retornará informações de monitoração das últimas cinco sessões do Merge Agent para essa assinatura. Observe o valor de **Session_id** para sessões de interesse no resultado definido.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md). Especifique um **Session_id** valor da etapa 1 para **@session_id**. Isso exibirá informações de monitoramento detalhadas sobre a sessão.  
  
3.  Repita a etapa 2 para cada sessão que interessar.  
  
#### Para exibir e modificar as métricas de limite do monitor para uma publicação  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md). Isso retornará o conjunto de limites de monitoramento, para todas as publicações que usam esse Distribuidor. Para limitar o conjunto de resultados para monitorar os limites das publicações pertencentes a um único publicador ou o banco de dados publicado ou para uma única publicação, especifique **@publisher**, **@publisher_db**, ou **@publication**, respectivamente. Observe o valor de **Metric_id** para os limites que devem ser alterados. Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md). Especifique o seguinte, quando necessário:  
  
    -   O **Metric_id** valor obtido na etapa 1 para **@metric_id**.  
  
    -   Um valor novo para a métrica de limite do monitor para **@value**.  
  
    -   O valor **1** para **@shouldalert** , para ser registrado um alerta, quando esse limite for atingido, ou o valor **0** , se não for necessário um alerta.  
  
    -   Um valor **1** para **@mode** , para habilitar a métrica de limite do monitor, ou um valor **2** para desabilitá-la.  
  
##  <a name="RMO"></a> RMO (Replication Management Objects)  
  
#### Para monitorar uma assinatura para uma publicação de mesclagem no Assinante  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> de classe e defina o <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> Propriedades para a assinatura e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
3.  Chame um dos métodos seguintes para retornar informações sobre as sessões do Merge Agent para essa assinatura:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -Retorna uma matriz de <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objetos com informações até as últimas cinco sessões do Merge Agent. Observação o <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> valor para todas as sessões de interesse.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -Retorna uma matriz de <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objetos com informações sobre sessões do Merge Agent que ocorreram durante o número de horas passado como o *horas* parâmetro (até as últimas cinco sessões). Observação o <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> valor para todas as sessões de interesse.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> -retorna um <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objeto com informações sobre a última sessão do Merge Agent. Observação o <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> valor para essa sessão.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> -retorna um <xref:System.Data.DataSet> objeto com informações até as últimas cinco sessões do Merge Agent, uma em cada linha. Observe o valor da **Session_id** coluna para todas as sessões de interesse.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> -retorna um <xref:System.Data.DataRow> objeto com informações sobre a última sessão do Merge Agent. Observe o valor da **Session_id** coluna para esta sessão.  
  
4.  (Opcional) Chamar <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> Para atualizar os dados para o <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> objeto passado como *mss,* ou chamar <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> para atualizar os dados a <xref:System.Data.DataRow> objeto passado como *drRefresh*.  
  
5.  Usando a id de sessão obtida na etapa 3, chame um dos métodos seguintes para retornar informações sobre os detalhes de uma sessão em particular:  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> -retorna uma matriz de <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> objetos para fornecido *SessionId*.  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> -retorna um <xref:System.Data.DataSet> objeto com informações especificado *SessionId*.  
  
#### Para monitorar as propriedades de replicação para todas as publicações em um Distribuidor  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto.  
  
5.  Execute um ou mais dos métodos seguintes para retornar informações de replicação para todos os Publicador que usam esse Distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os agentes de distribuição no distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre os erros armazenados no distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os agentes de leitor de Log no distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os agentes de mesclagem no distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os outros agentes de replicação no distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os publicadores neste distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> -retorna um <xref:System.Data.DataSet> objeto que retorna os publicadores que usam esse distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os agentes de leitor de fila no distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> -retorna um <xref:System.Data.DataSet> objeto que contém detalhes sobre o Queue Reader Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de sessão sobre o Queue Reader Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os agentes de instantâneo no distribuidor.  
  
#### Para monitorar as propriedades de publicação para um Publicador específico no Distribuidor  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Obtenha um <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto em uma das seguintes maneiras.  
  
    -   Criar uma instância do <xref:Microsoft.SqlServer.Replication.PublisherMonitor> classe. Definir o <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> propriedade do publicador e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, o nome do Publicador estava definido incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> acessados por meio do <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> propriedade de um objeto existente <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> objeto.  
  
3.  Execute um ou mais dos métodos a seguir para retornar informações de replicação para todas as publicações que pertençam a esse Publicador.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> -retorna um <xref:System.Data.DataSet> objeto que contém detalhes sobre o agente de distribuição e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de sessão sobre o agente de distribuição especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de registro de erro sobre o erro especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> -retorna um <xref:System.Data.DataSet> objeto que contém detalhes sobre o Log Reader Agent e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de sessão para o Log Reader Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> -retorna um <xref:System.Data.DataSet> objeto que contém detalhes sobre o agente de mesclagem e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> -retorna um <xref:System.Data.DataSet> objeto que contém detalhes adicionais sobre o agente de mesclagem e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de sessão para o Merge Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de sessão adicional para o Merge Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todas as publicações nesse distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações adicionais sobre todas as publicações nesse distribuidor.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> -retorna um <xref:System.Data.DataSet> objeto que contém detalhes sobre o agente de instantâneo e a sessão especificados.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de sessão para o Snapshot Agent especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todas as assinaturas para publicações nesse distribuidor.  
  
#### Para monitorar as propriedades para uma publicação específica no Distribuidor  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Obtenha um <xref:Microsoft.SqlServer.Replication.PublicationMonitor> objeto em uma das seguintes maneiras.  
  
    -   Criar uma instância do <xref:Microsoft.SqlServer.Replication.PublicationMonitor> classe. Definir o <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação foram definidas incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> acessados por meio do <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> propriedade de um objeto existente <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto.  
  
3.  Execute um ou mais dos métodos seguintes para retornar informações sobre essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> -retorna um <xref:System.Data.DataSet> objeto que contém registros de erro sobre o erro especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre o Log Reader Agent para essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre os limites de aviso do monitor definido para esta publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre o Queue Reader Agent usado por essa publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre o agente de instantâneo desta publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre assinaturas para esta publicação.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> -retorna um <xref:System.Data.DataSet> baseada em objeto que contém informações adicionais sobre as assinaturas dessa publicação em fornecido <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações de latência para o token de rastreamento especificado.  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> -retorna um <xref:System.Data.DataSet> objeto que contém informações sobre todos os tokens de rastreamento inseridos nessa publicação.  
  
#### Para monitorar os comandos transacionais que estão esperando para serem aplicados no Assinante.  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Obtenha um <xref:Microsoft.SqlServer.Replication.PublicationMonitor> objeto em uma das seguintes maneiras.  
  
    -   Criar uma instância do <xref:Microsoft.SqlServer.Replication.PublicationMonitor> classe. Definir o <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação foram definidas incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> acessados por meio do <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> propriedade de um objeto existente <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto.  
  
3.  Execute o <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> método, que retorna um <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> objeto.  
  
4.  Use as propriedades desse <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> objeto para determinar o número estimado de comandos pendentes e quanto tempo levará para completar a entrega desses comandos.  
  
#### Para definir os limites de aviso de monitoração para uma publicação  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Obtenha um <xref:Microsoft.SqlServer.Replication.PublicationMonitor> objeto em uma das seguintes maneiras.  
  
    -   Criar uma instância do <xref:Microsoft.SqlServer.Replication.PublicationMonitor> classe. Definir o <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, e <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> criado na etapa 1. Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação foram definidas incorretamente ou a publicação não existe.  
  
    -   Do <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> acessados por meio do <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> propriedade de um objeto existente <xref:Microsoft.SqlServer.Replication.PublisherMonitor> objeto.  
  
3.  Execute o <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> método. Observe as configurações de limite atuais no retornado <xref:System.Collections.ArrayList> de <xref:Microsoft.SqlServer.Replication.MonitorThreshold> objetos.  
  
4.  Execute o <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> método. Passe os seguintes parâmetros:  
  
    -   *metricID* - uma <xref:System.Int32> valor que representa a métrica de limite de monitoramento da tabela a seguir:  
  
        |Valor|Descrição|  
        |-----------|-----------------|  
        |1|**expiração** -monitora a expiração iminente de assinaturas para publicações transacionais.|  
        |2|**latência** -monitora o desempenho de assinaturas para publicações transacionais.|  
        |4|**mergeexpiration** -monitora a expiração iminente de assinaturas para publicações de mesclagem.|  
        |5|**mergeslowrunduration** -monitora a duração de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
        |6|**mergefastrunduration** -monitora a duração de sincronizações de mesclagem em conexões de alta largura de banda (LAN).|  
        |7|**mergefastrunspeed** -monitora a taxa de sincronizações de mesclagem em conexões de alta largura de banda (LAN).|  
        |8|**mergeslowrunspeed** -monitora a taxa de sincronizações de mesclagem em conexões de baixa largura de banda (discadas).|  
  
    -   *Habilitar* - <xref:System.Boolean> valor que indica se a métrica está habilitada para a publicação.  
  
    -   *thresholdValue* -valor inteiro que define o limite.  
  
    -   *shouldAlert* -inteiro que indica se esse limite deve gerar um alerta.  
  
  