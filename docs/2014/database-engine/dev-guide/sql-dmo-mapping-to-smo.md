---
title: Mapeamento de SQL-DMO para SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 31c9372674ab439c3435515c13f1d76518771328
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219266"
---
# <a name="sql-dmo-mapping-to-smo"></a>Mapeamento de SQL-DMO para SMO
  O SQL-DMO (SQL Distributed Management Objects) não faz mais parte do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]; os aplicativos do SQL-DMO devem ser convertidos para usar o SMO ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects). O modelo de objeto do SMO é semelhante ao do SQL-DMO, assim a maioria dos objetos do SQL-DMO é mapeada para um objeto com o mesmo nome no SMO. No entanto, alguns objetos do SQL-DMO foram alterados ou inseridos na transição para o SMO. Esta tabela lista a ação recomendada para usar os objetos do SQL-DMO que não foram convertidos diretamente em SMO.  
  
|Objeto do SQL-DMO|Ação no SMO|  
|---------------------|-------------------|  
|Objeto View2|Movido para o namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Objeto AlertSystem|Movido para o namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Objeto Application|Removido.|  
|Objeto Backup e Objeto Backup2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Backup> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objeto BackupDevice|Objetos <xref:Microsoft.SqlServer.Management.Smo.BackupDevice>|  
|Objeto BulkCopy e Objeto BulkCopy2|Removido e substituído pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Objeto Category|Movido para o namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>. Substituir pelos objetos <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory> e <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory>.|  
|Objeto Check|<xref:Microsoft.SqlServer.Management.Smo.Check> objeto|  
|Objeto Column e Objeto Column2|<xref:Microsoft.SqlServer.Management.Smo.Column> objeto.|  
|Objeto Configuration|Objetos <xref:Microsoft.SqlServer.Management.Smo.Configuration> e <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase>.|  
|Objeto ConfigValue|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> objeto.|  
|Objeto Database e Objeto Database2|<xref:Microsoft.SqlServer.Management.Smo.Database> objeto.|  
|Objeto DatabaseRole e Objeto DatabaseRole2|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> objeto.|  
|Objeto DBFile|<xref:Microsoft.SqlServer.Management.Smo.DataFile> objeto.|  
|Objeto DBOption e Objeto DBOption2|Movido para o objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions>.|  
|Objeto Default e Objeto Default2|<xref:Microsoft.SqlServer.Management.Smo.Default> objeto.|  
|Objeto DistributionArticle e Objeto DistributionArticle2|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto DistributionDatabase e Objeto DistributionDatabase2|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto DistributionPublication e Objeto DistributionPublication2|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto DistributionSubscription e Objeto DistributionSubscription2|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto Distributor e Objeto Distributor2|Movido para o <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto DRIDefault|Movido para <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> objeto.|  
|Objeto FileGroup e Objeto FileGroup2|<xref:Microsoft.SqlServer.Management.Smo.FileGroup> objeto.|  
|Objeto FullTextCatalog e Objeto FullTextCatalog2|Objetos <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> e <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex>.|  
|Objeto Index e Objeto Index2|<xref:Microsoft.SqlServer.Management.Smo.Index> objeto|  
|Objeto IntegratedSecurity|Funcionalidade movida para o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> no namespace <xref:Microsoft.SqlServer.Management.Common>.|  
|Objeto Job|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job> objeto. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto JobFilter|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter> objeto. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto JobHistoryFilter|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter> objeto. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto JobSchedule|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> objeto. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto JobServer e Objeto JobServer2|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> objeto. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto JobStep|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> objeto. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto Key|Objetos <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> e <xref:Microsoft.SqlServer.Management.Smo.Index>.|  
|Objeto LinkedServer e Objeto LinkedServer2|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto.|  
|Objeto LinkedServerLogin|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> objeto.|  
|Objeto LogFile|<xref:Microsoft.SqlServer.Management.Smo.LogFile> objeto.|  
|Objeto Login e Objeto Login2|<xref:Microsoft.SqlServer.Management.Smo.Login> objeto.|  
|Objeto MergeArticle e Objeto MergeArticle2|<xref:Microsoft.SqlServer.Replication.MergeArticle> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto MergeDynamicSnapshotJob|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto MergePublication e Objeto MergePublication2|<xref:Microsoft.SqlServer.Replication.MergePublication> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto MergePullSubscription e Objeto MergePullSubscription2|<xref:Microsoft.SqlServer.Replication.MergePullSubscription> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto MergeSubscription|<xref:Microsoft.SqlServer.Replication.MergeSubscription> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto MergeSubsetFilter|Movido para `N:Microsoft.SqlServer.Replication` namespace.|  
|Objeto NameList|Removido. Funcionalidade alternativa no objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter>.|  
|Objeto Operator|Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto Permission e Objeto Permission2|Objetos <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> e <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission>.|  
|Objeto Property|`Property` objeto.|  
|Objeto Publisher e Objeto Publisher2|<xref:Microsoft.SqlServer.Replication.ReplicationServer> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto QueryResults e Objeto QueryResults2|Substituído pelo objeto do sistema <xref:System.Data.DataTable> ou <xref:System.Data.DataSet>.|  
|Objeto RegisteredServer|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto RegisteredSubscriber|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto Registry e Objeto Registry2|Removido.|  
|Objeto RemoteLogin|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto. Movido para o namespace Common.|  
|Objeto RemoteServer e Objeto RemoteServer2|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto. Movido para <xref:Microsoft.SqlServer.Management.Common> namespace.|  
|Objeto Replication|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto ReplicationDatabase e Objeto ReplicationDatabase2|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto ReplicationSecurity|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto. Movido para <xref:Microsoft.SqlServer.Management.Common> namespace.|  
|Objeto ReplicationStoredProcedure e Objeto ReplicationStoredProcedure2|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto ReplicationTable e Objeto ReplicationTable2|<xref:Microsoft.SqlServer.Replication.ReplicationTable> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto Restore e Objeto Restore2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Restore> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objeto Rule e Objeto Rule2|<xref:Microsoft.SqlServer.Management.Smo.Rule> objeto|  
|Objeto Schedule|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto ServerGroup|Removido.|  
|Objeto ServerRole|<xref:Microsoft.SqlServer.Management.Smo.ServerRole> objeto.|  
|Objeto SQLObjectList|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> matriz.|  
|Objeto SQLServer e Objeto SQLServer2|<xref:Microsoft.SqlServer.Management.Smo.Server> objeto.|  
|Objeto StoredProcedure e Objeto StoredProcedure2|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> e <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> objetos|  
|Objeto Subscriber e Objeto Subscriber2|Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto SystemDatatype e Objeto SystemDataType2|<xref:Microsoft.SqlServer.Management.Smo.DataType> objeto.|  
|Objeto Table e Objeto Table2|<xref:Microsoft.SqlServer.Management.Smo.Table> objeto.|  
|Objeto TargetServer|Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto TargetServerGroup|Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> namespace.|  
|Objeto TransactionLog|Funcionalidade movida para o objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Objeto TransArticle e Objeto TransArticle2|<xref:Microsoft.SqlServer.Replication.TransArticle> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Método Transfer e Objeto Transfer2|<xref:Microsoft.SqlServer.Management.Smo.Transfer> objeto.|  
|Objeto TransPublication e Objeto TransPublication2|<xref:Microsoft.SqlServer.Replication.TransPublication> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto TransPullSubscription e Objeto TransPullSubscription2|<xref:Microsoft.SqlServer.Replication.TransPullSubscription> objeto. Movido para <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto Trigger e Objeto Trigger2|<xref:Microsoft.SqlServer.Management.Smo.Trigger> objeto.|  
|Objeto User e Objeto User2|<xref:Microsoft.SqlServer.Management.Smo.User> objeto.|  
|Objeto UserDefinedDatatype e Objeto UserDefinedDataType2|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> objeto.|  
|Objeto UserDefinedFunction|Objetos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>.|  
|Objeto View e Objeto View2|<xref:Microsoft.SqlServer.Management.Smo.View> objeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de Programação do SMO &#40;SQL Server Management Objects&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
