---
title: sys.availability_groups_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e552a4deb02e676905eefc470f220c6d54cdc5f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysavailabilitygroupscluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada grupo de disponibilidade AlwaysOn no Windows Server Failover WSFC (Clustering). Cada linha contém os metadados do grupo de disponibilidade do cluster do WSFC.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|GUID (identificador exclusivo) do grupo de disponibilidade.|  
|**name**|**sysname**|O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no WSFC (Windows Server Failover Cluster).|  
|**resource_id**|**nvarchar(40)**|ID de recurso do recurso de cluster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|ID do grupo de recursos do cluster WSFC do grupo de disponibilidade.|  
|**failure_condition_level**|**Int**|Nível de condição de falha definido pelo usuário no qual um failover automático deve ser disparado, um dos valores inteiros seguintes:<br /><br /> 1: Especifica que um failover automático deve ser iniciado quando o seguinte ocorre: <br />-A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço está inativo.<br />-A concessão do grupo de disponibilidade para conectar-se ao cluster de failover WSFC expira porque nenhum ACK foi recebido da instância de servidor. Para obter mais informações, veja [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> 2: Especifica que um failover automático deve ser iniciado quando o seguinte ocorre:  <br />-A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não se conectar ao cluster e o usuário especificado **health_check_timeout** limite do grupo de disponibilidade é excedido. <br />-A réplica de disponibilidade está em estado de falha. <br />3: Especifica que um failover automático deve ser iniciado em crítico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erros internos, como spinlocks órfãos, violações de acesso de gravação graves ou muito despejo. Este é o valor padrão. <br />4: Especifica que um failover automático deve ser iniciado em moderada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erros internos, como uma condição de falta de memória persistente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pool de recursos internos.<br />5: Especifica que um failover automático deve ser iniciado em qualquer condição de falha qualificada, incluindo:<br />-Esgotamento dos threads de trabalho do SQL Engine. <br />-Detecção de um deadlock insolúvel.<br /><br /> Os níveis da condição de falha (1 a 5) variam do menos restritivo, nível 1, até o mais restritivo, nível 5. Um determinado nível de condição abrange todos os níveis menos restritivos. Assim, o nível de condição mais rígido, 5, inclui os quatro níveis de condição menos restritivos (1 a 4), o nível 4 inclui os níveis 1 a 3 e assim sucessivamente.<br /><br /> Para alterar esse valor, use a opção FAILURE_CONDITION_LEVEL do [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.|  
|**health_check_timeout**|**Int**|Tempo de espera (em milissegundos) para o [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema de procedimento armazenado para retornar informações de integridade do servidor, antes da instância do servidor é considerada lenta ou suspenso. O valor padrão é 30000 milissegundos (30 segundos).<br /><br /> Para alterar esse valor, use a opção HEALTH_CHECK_TIMEOUT da [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.|  
|**automated_backup_preference**|**tinyint**|Local preferido para executar backups nos bancos de dados de disponibilidade nesse grupo de disponibilidade. Um dos valores seguintes:<br /><br /> 0: principal. Backups sempre devem ocorrer na réplica primária.<br />1: somente secundária. A execução de backups em uma réplica secundária é preferível.<br />2: preferir secundário. A execução de backups em uma réplica secundária é preferível, mas a execução de backups na réplica primária será aceitável se nenhuma réplica secundária estiver disponível para operações de backup. Esse é o comportamento padrão.<br />3: qualquer réplica. Nenhuma preferência sobre se os backups são executados na réplica primária ou em uma réplica secundária.<br /><br /> Para obter mais informações, consulte [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Descrição do **automated_backup_preference**, um de:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Nenhuma|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION na instância de servidor.  
  
## <a name="see-also"></a>Consulte também  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
