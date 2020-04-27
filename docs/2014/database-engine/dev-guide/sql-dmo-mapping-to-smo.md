---
title: Mapeamento de SQL-DMO para SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a6273032f88807291bfc7024f1abcdbd1440073
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62780676"
---
# <a name="sql-dmo-mapping-to-smo"></a>Mapeamento de SQL-DMO para SMO
  O SQL-DMO (SQL Distributed Management Objects) não faz mais parte do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]; os aplicativos do SQL-DMO devem ser convertidos para usar o SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects). O modelo de objeto do SMO é semelhante ao do SQL-DMO, assim a maioria dos objetos do SQL-DMO é mapeada para um objeto com o mesmo nome no SMO. No entanto, alguns objetos do SQL-DMO foram alterados ou inseridos na transição para o SMO. Esta tabela lista a ação recomendada para usar os objetos do SQL-DMO que não foram convertidos diretamente em SMO.  
  
|Objeto do SQL-DMO|Ação no SMO|  
|---------------------|-------------------|  
|Objeto View2|Movido para o namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Objeto AlertSystem|Movido para o namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Objeto Application|Removido.|  
|Objeto Backup e Objeto Backup2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Backup> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objeto BackupDevice|Objetos <xref:Microsoft.SqlServer.Management.Smo.BackupDevice>|  
|Objeto BulkCopy e Objeto BulkCopy2|Removido e substituído pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Objeto Category|Movido para o namespace <xref:Microsoft.SqlServer.Management.Smo.Agent>. Substituir pelos objetos <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory> e <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory>.|  
|Objeto Check|Objeto <xref:Microsoft.SqlServer.Management.Smo.Check>|  
|Objeto Column e Objeto Column2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Column>.|  
|Objeto Configuration|Objetos <xref:Microsoft.SqlServer.Management.Smo.Configuration> e <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase>.|  
|Objeto ConfigValue|Objeto <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>.|  
|Objeto Database e Objeto Database2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Objeto DatabaseRole e Objeto DatabaseRole2|Objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole>.|  
|Objeto DBFile|Objeto <xref:Microsoft.SqlServer.Management.Smo.DataFile>.|  
|Objeto DBOption e Objeto DBOption2|Movido para o objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions>.|  
|Objeto Default e Objeto Default2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Default>.|  
|Objeto DistributionArticle e Objeto DistributionArticle2|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto DistributionDatabase e Objeto DistributionDatabase2|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto DistributionPublication e Objeto DistributionPublication2|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto DistributionSubscription e Objeto DistributionSubscription2|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto Distributor e Objeto Distributor2|Movido para o <xref:Microsoft.SqlServer.Replication> namespace.|  
|Objeto DRIDefault|Movido para <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> o objeto.|  
|Objeto FileGroup e Objeto FileGroup2|Objeto <xref:Microsoft.SqlServer.Management.Smo.FileGroup>.|  
|Objeto FullTextCatalog e Objeto FullTextCatalog2|Objetos <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> e <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex>.|  
|Objeto Index e Objeto Index2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Index>|  
|Objeto IntegratedSecurity|Funcionalidade movida para o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> no namespace <xref:Microsoft.SqlServer.Management.Common>.|  
|Objeto Job|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.Job>. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto JobFilter|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter>. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto JobHistoryFilter|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter>. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto JobSchedule|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule>. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto JobServer e Objeto JobServer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer>. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto JobStep|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep>. Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto Key|Objetos <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> e <xref:Microsoft.SqlServer.Management.Smo.Index>.|  
|Objeto LinkedServer e Objeto LinkedServer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>.|  
|Objeto LinkedServerLogin|Objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>.|  
|Objeto LogFile|Objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>.|  
|Objeto Login e Objeto Login2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Login>.|  
|Objeto MergeArticle e Objeto MergeArticle2|Objeto <xref:Microsoft.SqlServer.Replication.MergeArticle>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto MergeDynamicSnapshotJob|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto MergePublication e Objeto MergePublication2|Objeto <xref:Microsoft.SqlServer.Replication.MergePublication>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto MergePullSubscription e Objeto MergePullSubscription2|Objeto <xref:Microsoft.SqlServer.Replication.MergePullSubscription>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto MergeSubscription|Objeto <xref:Microsoft.SqlServer.Replication.MergeSubscription>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto MergeSubsetFilter|Movido para `N:Microsoft.SqlServer.Replication` o namespace.|  
|Objeto NameList|Removido. Funcionalidade alternativa no objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter>.|  
|Objeto Operator|Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto Permission e Objeto Permission2|Objetos <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> e <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission>.|  
|Objeto Property|Objeto `Property`.|  
|Objeto Publisher e Objeto Publisher2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto QueryResults e Objeto QueryResults2|Substituído pelo objeto do sistema <xref:System.Data.DataTable> ou <xref:System.Data.DataSet>.|  
|Objeto RegisteredServer|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto RegisteredSubscriber|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto Registry e Objeto Registry2|Removido.|  
|Objeto RemoteLogin|Objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Movido para o namespace Common.|  
|Objeto RemoteServer e Objeto RemoteServer2|Objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Movido para <xref:Microsoft.SqlServer.Management.Common> o namespace.|  
|Objeto Replication|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto ReplicationDatabase e Objeto ReplicationDatabase2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationDatabase>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto ReplicationSecurity|Objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Movido para <xref:Microsoft.SqlServer.Management.Common> o namespace.|  
|Objeto ReplicationStoredProcedure e Objeto ReplicationStoredProcedure2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto ReplicationTable e Objeto ReplicationTable2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationTable>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto Restore e Objeto Restore2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Restore> e <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objeto Rule e Objeto Rule2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>|  
|Objeto Schedule|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto ServerGroup|Removido.|  
|Objeto ServerRole|Objeto <xref:Microsoft.SqlServer.Management.Smo.ServerRole>.|  
|Objeto SQLObjectList|Matriz <xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject>.|  
|Objeto SQLServer e Objeto SQLServer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.|  
|Objeto StoredProcedure e Objeto StoredProcedure2|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>e <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> objetos|  
|Objeto Subscriber e Objeto Subscriber2|Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto SystemDatatype e Objeto SystemDataType2|Objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>.|  
|Objeto Table e Objeto Table2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.|  
|Objeto TargetServer|Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto TargetServerGroup|Movido para <xref:Microsoft.SqlServer.Management.Smo.Agent> o namespace.|  
|Objeto TransactionLog|Funcionalidade movida para o objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Objeto TransArticle e Objeto TransArticle2|Objeto <xref:Microsoft.SqlServer.Replication.TransArticle>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Método Transfer e Objeto Transfer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Objeto TransPublication e Objeto TransPublication2|Objeto <xref:Microsoft.SqlServer.Replication.TransPublication>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto TransPullSubscription e Objeto TransPullSubscription2|Objeto <xref:Microsoft.SqlServer.Replication.TransPullSubscription>. Movido para <xref:Microsoft.SqlServer.Replication> o namespace.|  
|Objeto Trigger e Objeto Trigger2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>.|  
|Objeto User e Objeto User2|Objeto <xref:Microsoft.SqlServer.Management.Smo.User>.|  
|Objeto UserDefinedDatatype e Objeto UserDefinedDataType2|Objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>.|  
|Objeto UserDefinedFunction|Objetos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>.|  
|Objeto View e Objeto View2|Objeto <xref:Microsoft.SqlServer.Management.Smo.View>.|  
  
## <a name="see-also"></a>Consulte Também  
 [Guia de Programação do SMO &#40;SQL Server Management Objects&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
