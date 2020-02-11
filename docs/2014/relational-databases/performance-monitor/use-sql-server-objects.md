---
title: Usar objetos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- server performance [SQL Server], objects for monitoring
- database monitoring [SQL Server], objects for monitoring
- charts [SQL Server]
- System Monitor [SQL Server], counters
- counters [SQL Server], listed
- objects [SQL Server], performance monitoring
- objects [SQL Server], Windows System Monitor
- performance counters [SQL Server], about performance counters
- System Monitor [SQL Server], objects
- performance counters [SQL Server]
- counters [SQL Server], about performance counters
- tuning databases [SQL Server], objects for monitoring
- database performance [SQL Server], objects for monitoring
- SQL Server, objects
- monitoring performance [SQL Server], objects for monitoring
- Windows System Monitor [SQL Server], objects
- Windows System Monitor [SQL Server], counters
- counters [SQL Server]
- performance counters [SQL Server], listed
ms.assetid: bcd731b1-3c4e-4086-b58a-af7a3af904ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67edebf9b4adcf40c12190446997dbd7c4b6e57b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151168"
---
# <a name="use-sql-server-objects"></a>Usar objetos do SQL Server
  O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor do Sistema para monitorar a atividade em computadores que executem uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um objeto é qualquer recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como um bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um processo do Windows. Cada objeto contém um ou mais contadores, que determinam vários aspectos dos objetos a monitorar. Por exemplo, o objeto **SQL Server Locks** contém contadores chamados **Número de deadlocks/segundo** e **Tempos limite de bloqueio/segundo**.  
  
 Alguns objetos terão várias instâncias se existirem vários recursos de um determinado tipo no computador. Por exemplo, o tipo de objeto **Processor** terá várias instâncias se o sistema tiver vários processadores. O tipo de objeto **Databases** tem uma instância para cada banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Alguns tipos de objeto (por exemplo, o objeto **Memory Manager** ) têm só uma instância. Se um tipo de objeto tiver várias instâncias, você poderá adicionar contadores para rastrear as estatísticas de cada instância ou, em muitos casos, de todas as instâncias de uma só vez. Os contadores da instância padrão aparecem no formato **SQLServer:** _\<object name>_ . Os contadores das instâncias nomeadas aparecem no formato **MSSQL$** _\<<instance name_ **:** _\<counter name>_ ou **SQLAgent$** _\<instance name>_ **:** _\<counter name>_ .  
  
 Adicionando ou removendo contadores do gráfico e salvando as configurações deste, é possível especificar objetos e contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorados quando o Monitor do Sistema é iniciado.  
  
 É possível configurar o Monitor do Sistema para que exiba estatísticas de qualquer contador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Além disso, é possível definir um valor de limite para qualquer contador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gerar um alerta quando o contador ultrapassar esse limite. Para obter mais informações sobre como definir um alerta, veja [Criar um alerta do Banco de Dados SQL Server](create-a-sql-server-database-alert.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são exibidas apenas quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalada. Se você parar e reiniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a exibição de estatísticas será interrompida e retomada automaticamente. Observe, ainda, que serão vistos contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no snap-in do Monitor do Sistema mesmo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não esteja em execução. Em uma instância clusterizada, os contadores de desempenho só funcionam no nó de execução do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Este tópico contém as seguintes seções:  
  
-   [Objetos de desempenho do SQL Server Agent](#SQLServerAgentPOs)  
  
-   [Objetos de desempenho do Service Broker](#ServiceBrokerPOs)  
  
-   [Objetos de desempenho do SQL Server](#SQLServerPOs)  
  
-   [Objetos de desempenho de replicação do SQL Server](#SQLServerReplicationPOs)  
  
-   [Contadores de pipeline SSIS](#SsisPipelineCounters)  
  
-   [Permissões necessárias](#RequiredPermissions)  
  
##  <a name="SQLServerAgentPOs"></a> Objetos de desempenho do SQL Server Agent  
 A seguinte tabela lista os objetos de desempenho oferecidos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
|Objeto de desempenho|DESCRIÇÃO|  
|------------------------|-----------------|  
|[SQLAgent:Alerts](sql-server-agent-alerts-object.md)|Fornece informações sobre alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:Jobs](sql-server-agent-jobs-object.md)|Fornece informações sobre trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:JobSteps](sql-server-agent-jobsteps-object.md)|Fornece informações sobre etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:Statistics](sql-server-agent-statistics-object.md)|Fornece informações gerais sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
  
##  <a name="ServiceBrokerPOs"></a> Objetos de desempenho do Service Broker  
 A tabela a seguir lista os objetos de desempenho oferecidos para o [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
|Objeto de desempenho|DESCRIÇÃO|  
|------------------------|-----------------|  
|[SQLServer:Broker Activation](sql-server-broker-activation-object.md)|Fornece informações sobre tarefas ativadas pelo [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|[SQLServer:Broker Statistics](sql-server-broker-statistics-object.md)|Fornece informações gerais sobre o [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
|[SQLServer:Broker Transport](sql-server-broker-dbm-transport-object.md)|Fornece informações sobre o sistema de redes do [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
  
##  <a name="SQLServerPOs"></a> Objetos de desempenho do SQL Server  
 A tabela a seguir descreve objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de desempenho|DESCRIÇÃO|  
|------------------------|-----------------|  
|[SQLServer:Métodos de Acesso](sql-server-access-methods-object.md)|Pesquisa e mede a alocação de objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, o número de pesquisas de índice ou número de páginas alocadas para índices e dados).|  
|[SQLServer:Backup Device](sql-server-backup-device-object.md)|Fornece informações sobre dispositivos de backup usados para operações de backup e restauração, como a taxa de transferência do dispositivo backup.|  
|[SQLServer:Buffer Manager](sql-server-buffer-manager-object.md)|Fornece informações sobre os buffers de memória usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como **freememory** (memória livre) e **buffer cache hit ratio**(taxa de acertos de cache do buffer).|  
|[SQL Server:Buffer Node](sql-server-buffer-node.md)|Fornece informações sobre a frequência com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita e acessa páginas livres.|  
|[SQLServer:CLR](sql-server-clr-object.md)|Fornece informações sobre CLR (Common Language Runtime).|  
|[SQLServer:Cursor Manager by Type](sql-server-cursor-manager-by-type-object.md)|Fornece informações sobre cursores.|  
|[SQLServer:Cursor Manager Total](sql-server-cursor-manager-total-object.md)|Fornece informações sobre cursores.|  
|[SQLServer:Database Mirroring](sql-server-database-mirroring-object.md)|Fornece informações sobre espelhamento de banco de dados.|  
|[SQLServer:Databases](sql-server-databases-object.md)|Fornece informações sobre um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como a quantidade de espaço de log livre disponível ou o número de transações ativas no banco de dados. Pode haver várias instâncias deste objeto.|  
|[SQL Server:Deprecated Features](sql-server-deprecated-features-object.md)|Conta quantas vezes foram utilizados recursos preteridos.|  
|[SQLServer:Exec Statistics](sql-server-execstatistics-object.md)|Fornece informações sobre estatísticas de execução.|  
|[SQLServer:General Statistics](sql-server-general-statistics-object.md)|Fornece informações sobre a atividade geral em todo o servidor, como o número de usuários conectados a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server:HADR Availability Replica](sql-server-availability-replica.md)|Fornece informações sobre alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQL Server:HADR Database Replica](sql-server-database-replica.md)|Fornece informações sobre as réplicas do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQLServer:Latches](sql-server-latches-object.md)|Fornece informações sobre as travas em recursos internos, como páginas de banco de dados, utilizadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Locks](sql-server-locks-object.md)|Fornece informações sobre as solicitações de bloqueio individuais feitas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como tempos limite de bloqueio e deadlocks. Pode haver várias instâncias deste objeto.|  
|[SQLServer:Memory Manager](sql-server-memory-manager-object.md)|Fornece informações sobre o uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como o número total de estruturas de bloqueio alocadas atualmente.|  
|[SQLServer:Cache de planos](sql-server-plan-cache-object.md)|Fornece informações sobre o cache do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizado para armazenar objetos, como procedimentos armazenados, gatilhos e planos de consulta.|  
|[SQLServer:Estatísticas de Pool de Recursos](sql-server-resource-pool-stats-object.md)|Contém informações sobre estatísticas de pool de recursos do Administrador de Recursos.|  
|[SQLServer:SQL Errors](sql-server-sql-errors-object.md)|Fornece informações sobre erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLServer:SQL Statistics](sql-server-sql-statistics-object.md)|Fornece informações sobre aspectos de consultas do [!INCLUDE[tsql](../../includes/tsql-md.md)] , como o número de lotes de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] recebidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Transactions](sql-server-transactions-object.md)|Fornece informações sobre as transações ativas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o número global de transações e o número de transações de instantâneo.|  
|[SQLServer:User Settable](sql-server-user-settable-object.md)|Executa monitoramento personalizado. Cada contador pode ser um procedimento armazenado personalizado ou qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que retorne um valor a ser monitorado.|  
|[SQLServer: Estatísticas de Espera](sql-server-wait-statistics-object.md)|Fornece informações sobre esperas.|  
|[SQLServer: Estatísticas de Grupo de Cargas de Trabalho](sql-server-workload-group-stats-object.md)|Contém informações sobre estatísticas de grupo de cargas de trabalho do Administrador de Recursos.|  
  
##  <a name="SQLServerReplicationPOs"></a> Objetos de desempenho de replicação do SQL Server  
 A seguinte tabela lista os objetos de desempenho fornecidos para replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Objeto de desempenho|DESCRIÇÃO|  
|------------------------|-----------------|  
|**SQLServer:Replication Agents**<br /><br /> **SQLServer:Replication Snapshot**<br /><br /> **SQLServer:Replication Logreader**<br /><br /> **SQLServer:Replication Dist.**<br /><br /> **SQLServer:Replication Merge**<br /><br /> Para obter mais informações, consulte [Monitoring Replication with System Monitor](../replication/monitor/monitoring-replication-with-system-monitor.md).|Fornece informações sobre a atividade do agente de replicação.|  
  
##  <a name="SsisPipelineCounters"></a> Contadores de pipeline SSIS  
 Para o contador **Pipeline do SSIS** , veja [Contadores de desempenho](../../integration-services/performance/performance-counters.md).  
  
##  <a name="RequiredPermissions"></a> Permissões necessárias  
 O uso dos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de permissões do Windows, exceto no caso de **SQLAgent:Alerts**. Os usuários devem ser membros da função de servidor fixa **sysadmin** para poderem usar **SQLAgent:Alerts**.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
