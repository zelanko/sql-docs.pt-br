---
title: Usar objetos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: 995728047e02ccf2127ba8c85949bde3031007dd
ms.sourcegitcommit: fff9db8affb094a8cce9d563855955ddc1af42d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49324619"
---
# <a name="use-sql-server-objects"></a>Usar objetos do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor do Sistema para monitorar a atividade em computadores que executem uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um objeto é qualquer recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como um bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um processo do Windows. Cada objeto contém um ou mais contadores, que determinam vários aspectos dos objetos a monitorar. Por exemplo, o objeto **SQL Server Locks** contém contadores chamados **Número de deadlocks/segundo** e **Tempos limite de bloqueio/segundo**.  
  
 Alguns objetos terão várias instâncias se existirem vários recursos de um determinado tipo no computador. Por exemplo, o tipo de objeto **Processor** terá várias instâncias se o sistema tiver vários processadores. O tipo de objeto **Databases** tem uma instância para cada banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Alguns tipos de objeto (por exemplo, o objeto **Memory Manager** ) têm só uma instância. Se um tipo de objeto tiver várias instâncias, você poderá adicionar contadores para rastrear as estatísticas de cada instância ou, em muitos casos, de todas as instâncias de uma só vez. Os contadores da instância padrão aparecem no formato **SQLServer:***\<object name>*. Os contadores das instâncias nomeadas aparecem no formato **MSSQL$***\<nome da instância>***:***\<nome do contador>* ou **SQLAgent$***\<nome da instância>***:***\<nome do contador>*.  
  
 Adicionando ou removendo contadores do gráfico e salvando as configurações deste, é possível especificar objetos e contadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorados quando o Monitor do Sistema é iniciado.  
  
 É possível configurar o Monitor do Sistema para que exiba estatísticas de qualquer contador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Além disso, é possível definir um valor de limite para qualquer contador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gerar um alerta quando o contador ultrapassar esse limite. Para obter mais informações sobre como definir um alerta, veja [Criar um alerta do Banco de Dados SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md).  
  
> [!TIP]  
>  Também é possível retornar valores de contador de desempenho consultando a exibição de gerenciamento dinâmico [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) .  
  
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
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|Fornece informações sobre alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|Fornece informações sobre trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|Fornece informações sobre etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|Fornece informações gerais sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
  
##  <a name="ServiceBrokerPOs"></a> Objetos de desempenho do Service Broker  
 A tabela a seguir lista os objetos de desempenho oferecidos para o [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|[SQLServer:Broker Activation](../../relational-databases/performance-monitor/sql-server-broker-activation-object.md)|Fornece informações sobre tarefas ativadas pelo [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|[SQLServer:Broker Statistics](../../relational-databases/performance-monitor/sql-server-broker-statistics-object.md)|Fornece informações gerais sobre o [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
|[SQLServer:Broker Transport](../../relational-databases/performance-monitor/sql-server-broker-dbm-transport-object.md)|Fornece informações sobre o sistema de redes do [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
  
##  <a name="SQLServerPOs"></a> Objetos de desempenho do SQL Server  
 A tabela a seguir descreve objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|[SQLServer:Métodos de Acesso](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)|Pesquisa e mede a alocação de objetos de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, o número de pesquisas de índice ou número de páginas alocadas para índices e dados).|  
|[SQLServer:Backup Device](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)|Fornece informações sobre dispositivos de backup usados para operações de backup e restauração, como a taxa de transferência do dispositivo backup.|  
|[SQLServer:Batch Resp Statistics](../../relational-databases/performance-monitor/sql-server-batch-resp-statistics-object.md)|Contadores para acompanhar tempos de resposta de Lote SQL.| 
|[SQLServer:Buffer Manager](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|Fornece informações sobre os buffers de memória usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como **freememory** (memória livre) e **buffer cache hit ratio**(taxa de acertos de cache do buffer).|  
|[SQL Server:Buffer Node](../../relational-databases/performance-monitor/sql-server-buffer-node.md)|Fornece informações sobre a frequência com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita e acessa páginas livres.|  
|[SQLServer:Metadados de Catálogo](../../relational-databases/performance-monitor/sql-server-catalog-metadata-object.md)|Define um objeto gerenciador de metadados de catálogo para o SQL Server.| 
|[SQLServer:CLR](../../relational-databases/performance-monitor/sql-server-clr-object.md)|Fornece informações sobre CLR (Common Language Runtime).|  
|[SQLServer:Columnstore](../../relational-databases/performance-monitor/sql-server-columnstore-object.md)|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> Fornece informações sobre rowgroups e segmentos para índices columnstore.|  
|[SQLServer:Cursor Manager by Type](../../relational-databases/performance-monitor/sql-server-cursor-manager-by-type-object.md)|Fornece informações sobre cursores.|  
|[SQLServer:Cursor Manager Total](../../relational-databases/performance-monitor/sql-server-cursor-manager-total-object.md)|Fornece informações sobre cursores.|  
|[SQLServer:Database Mirroring](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)|Fornece informações sobre espelhamento de banco de dados.|  
|[SQLServer:Databases](../../relational-databases/performance-monitor/sql-server-databases-object.md)|Fornece informações sobre um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como a quantidade de espaço de log livre disponível ou o número de transações ativas no banco de dados. Pode haver várias instâncias deste objeto.|  
|[SQL Server:Deprecated Features](../../relational-databases/performance-monitor/sql-server-deprecated-features-object.md)|Conta quantas vezes foram utilizados recursos preteridos.|  
|[SQLServer:Exec Statistics](../../relational-databases/performance-monitor/sql-server-execstatistics-object.md)|Fornece informações sobre estatísticas de execução.|  
|[SQL Server: Scripts Externos](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> Fornece informações sobre a execução do script externo.|  
|[SQLServer:FileTable](../../relational-databases/performance-monitor/sql-server-filetable-object.md)|Estatísticas associadas a FileTable e a acesso não transacionado.|  
|[SQLServer:General Statistics](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)|Fornece informações sobre a atividade geral em todo o servidor, como o número de usuários conectados a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server:HADR Availability Replica](../../relational-databases/performance-monitor/sql-server-availability-replica.md)|Fornece informações sobre alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQL Server:HADR Database Replica](../../relational-databases/performance-monitor/sql-server-database-replica.md)|Fornece informações sobre as réplicas do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQL Server: Armazenamento HTTP](../../relational-databases/performance-monitor/sql-server-http-storage-object.md)|Fornece informações para monitorar uma conta de Armazenamento do Microsoft Azure ao usar [Arquivos de Dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)|  
|[SQLServer:Latches](../../relational-databases/performance-monitor/sql-server-latches-object.md)|Fornece informações sobre as travas em recursos internos, como páginas de banco de dados, utilizadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Locks](../../relational-databases/performance-monitor/sql-server-locks-object.md)|Fornece informações sobre as solicitações de bloqueio individuais feitas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como tempos limite de bloqueio e deadlocks. Pode haver várias instâncias deste objeto.|  
|[SQLServer:LogPool FreePool](../../relational-databases/performance-monitor/sql-server-logpool-freepool-object.md)|Descreve as estatísticas para o pool livre dentro do Pool de Logs.|
|[SQLServer:Administradores do Agente de Memória](../../relational-databases/performance-monitor/sql-server-memory-broker-clerks-object.md)|Estatísticas relacionadas a administradores de agente de memória.|
|[SQLServer:Memory Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)|Fornece informações sobre o uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como o número total de estruturas de bloqueio alocadas atualmente.|  
|[SQLServer:Cache de planos](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)|Fornece informações sobre o cache do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizado para armazenar objetos, como procedimentos armazenados, gatilhos e planos de consulta.|  
|[SQL Server: Repositório de Consultas](../../relational-databases/performance-monitor/sql-server-query-store-object.md)|Fornece informações sobre o Repositório de Consultas.|  
|[SQLServer:Estatísticas de Pool de Recursos](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)|Contém informações sobre estatísticas de pool de recursos do Administrador de Recursos.|  
|[SQLServer:SQL Errors](../../relational-databases/performance-monitor/sql-server-sql-errors-object.md)|Fornece informações sobre erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLServer:SQL Statistics](../../relational-databases/performance-monitor/sql-server-sql-statistics-object.md)|Fornece informações sobre aspectos de consultas do [!INCLUDE[tsql](../../includes/tsql-md.md)] , como o número de lotes de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] recebidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Transactions](../../relational-databases/performance-monitor/sql-server-transactions-object.md)|Fornece informações sobre as transações ativas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o número global de transações e o número de transações de instantâneo.|  
|[SQLServer:User Settable](../../relational-databases/performance-monitor/sql-server-user-settable-object.md)|Executa monitoramento personalizado. Cada contador pode ser um procedimento armazenado personalizado ou qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que retorne um valor a ser monitorado.|  
|[SQLServer: Estatísticas de Espera](../../relational-databases/performance-monitor/sql-server-wait-statistics-object.md)|Fornece informações sobre esperas.|  
|[SQLServer: Estatísticas de Grupo de Cargas de Trabalho](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)|Contém informações sobre estatísticas de grupo de cargas de trabalho do Administrador de Recursos.|  
  
##  <a name="SQLServerReplicationPOs"></a> Objetos de desempenho de replicação do SQL Server  
 A seguinte tabela lista os objetos de desempenho fornecidos para replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|**SQLServer:Replication Agents**<br /><br /> **SQLServer:Replication Snapshot**<br /><br /> **SQLServer:Replication Logreader**<br /><br /> **SQLServer:Replication Dist.**<br /><br /> **SQLServer:Replication Merge**<br /><br /> Para obter mais informações, consulte [Monitoring Replication with System Monitor](../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).|Fornece informações sobre a atividade do agente de replicação.|  
  
##  <a name="SsisPipelineCounters"></a> Contadores de pipeline SSIS  
 Para o contador **Pipeline do SSIS** , veja [Contadores de desempenho](../../integration-services/performance/performance-counters.md).  
  
##  <a name="RequiredPermissions"></a> Permissões necessárias  
 O uso dos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de permissões do Windows, exceto no caso de **SQLAgent:Alerts**. Os usuários devem ser membros da função de servidor fixa **sysadmin** para poderem usar **SQLAgent:Alerts**.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
