---
description: sys.availability_groups_cluster (Transact-SQL)
title: sys. availability_groups_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8cdbb0b871da55eddaaf2a9266679de4a9c8ee19
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490378"
---
# <a name="sysavailability_groups_cluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada grupo de disponibilidade Always On no WSFC (Windows Server Failover Clustering). Cada linha contém os metadados do grupo de disponibilidade do cluster do WSFC.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|GUID (identificador exclusivo) do grupo de disponibilidade.|  
|**name**|**sysname**|O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no WSFC (Windows Server Failover Cluster).|  
|**resource_id**|**nvarchar(40)**|ID de recurso do recurso de cluster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|ID do grupo de recursos do cluster WSFC do grupo de disponibilidade.|  
|**failure_condition_level**|**int**|Nível de condição de falha definido pelo usuário no qual um failover automático deve ser disparado, um dos valores inteiros seguintes:<br /><br /> 1: Especifica que um failover automático deve ser iniciado quando qualquer uma das seguintes situações ocorrer: <br />-O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço está inoperante.<br />-A concessão do grupo de disponibilidade para se conectar ao cluster de failover do WSFC expira porque nenhuma confirmação é recebida da instância do servidor. Para obter mais informações, confira [Como funciona: Tempo limite de concessão do Always On do SQL Server](https://techcommunity.microsoft.com/t5/sql-server-support/how-it-works-sql-server-alwayson-lease-timeout/ba-p/317268).<br /><br /> 2: Especifica que um failover automático deve ser iniciado quando qualquer uma das seguintes situações ocorrer:  <br />-A instância do não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta ao cluster e o limite de **health_check_timeout** especificado pelo usuário do grupo de disponibilidade foi excedido. <br />-A réplica de disponibilidade está em estado de falha. <br />3: Especifica que um failover automático deve ser iniciado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erros internos críticos, como spinlocks órfãos, violações graves de acesso de gravação ou excesso de despejo. Este é o valor padrão. <br />4: Especifica que um failover automático deve ser iniciado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erros internos moderados, como uma condição de memória insuficiente persistente no pool de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos interno.<br />5: Especifica que um failover automático deve ser iniciado em qualquer condição de falha qualificada, incluindo:<br />-Esgotamento do trabalho do mecanismo do SQL-threads. <br />-Detecção de um deadlock não resolvivel.<br /><br /> Os níveis da condição de falha (1 a 5) variam do menos restritivo, nível 1, até o mais restritivo, nível 5. Um determinado nível de condição abrange todos os níveis menos restritivos. Assim, o nível de condição mais rígido, 5, inclui os quatro níveis de condição menos restritivos (1 a 4), o nível 4 inclui os níveis 1 a 3 e assim sucessivamente.<br /><br /> Para alterar esse valor, use a opção FAILURE_CONDITION_LEVEL da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**health_check_timeout**|**int**|Tempo de espera (em milissegundos) para o procedimento armazenado do sistema [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) para retornar informações de integridade do servidor, antes que a instância do servidor seja considerada lenta ou não está respondendo. O valor padrão é 30000 milissegundos (30 segundos).<br /><br /> Para alterar esse valor, use a opção HEALTH_CHECK_TIMEOUT da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**automated_backup_preference**|**tinyint**|Local preferido para executar backups nos bancos de dados de disponibilidade nesse grupo de disponibilidade. Um dos seguintes valores:<br /><br /> 0: primário. Backups sempre devem ocorrer na réplica primária.<br />1: somente secundário. A execução de backups em uma réplica secundária é preferível.<br />2: preferir secundário. A execução de backups em uma réplica secundária é preferível, mas a execução de backups na réplica primária será aceitável se nenhuma réplica secundária estiver disponível para operações de backup. Esse é o comportamento padrão.<br />3: qualquer réplica. Nenhuma preferência sobre se os backups são executados na réplica primária ou em uma réplica secundária.<br /><br /> Para obter mais informações, confira [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Descrição de **automated_backup_preference**, uma das:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Nenhuma|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION na instância de servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;&#41;Transact-SQL ](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
