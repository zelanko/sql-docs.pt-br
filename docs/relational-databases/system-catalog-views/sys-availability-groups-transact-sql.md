---
title: sys. availability_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ca82c64d2d0269564567de175b9d6f778f76d4d7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70874259"
---
# <a name="sysavailability_groups-transact-sql"></a>sys.availability_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada grupo de disponibilidade para o qual a instância local do SQL Server hospeda uma réplica de disponibilidade. Cada linha contém uma cópia armazenada em cache dos metadados do grupo de disponibilidade.  
   
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|GUID (identificador exclusivo) do grupo de disponibilidade.|  
|**name**|**sysname**|O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no WSFC (Windows Server Failover Cluster).|  
|**resource_id**|**nvarchar(40)**|ID de recurso do recurso de cluster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|ID do grupo de recursos do cluster WSFC do grupo de disponibilidade.|  
|**failure_condition_level**|**int**|Nível de condição de falha definido pelo usuário sob o qual um failover automático deve ser disparado, um dos valores inteiros mostrados na tabela imediatamente abaixo dessa tabela.<br /><br /> Os níveis da condição de falha (1 a 5) variam do menos restritivo, nível 1, até o mais restritivo, nível 5. Um determinado nível de condição abrange todos os níveis menos restritivos. Assim, o nível de condição mais rígido, 5, inclui os quatro níveis de condição menos restritivos (1 a 4), o nível 4 inclui os níveis 1 a 3 e assim sucessivamente.<br /><br /> Para alterar esse valor, use a opção FAILURE_CONDITION_LEVEL da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**health_check_timeout**|**int**|Tempo de espera (em milissegundos) para o procedimento armazenado do sistema [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) para retornar informações de integridade do servidor, antes que a instância do servidor seja considerada lenta ou não está respondendo. O valor padrão é 30000 milissegundos (30 segundos).<br /><br /> Para alterar esse valor, use a opção HEALTH_CHECK_TIMEOUT da instrução [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**automated_backup_preference**|**tinyint**|Local preferido para executar backups nos bancos de dados de disponibilidade nesse grupo de disponibilidade. A seguir estão os possíveis valores e suas descrições.<br /><br /> <br /><br /> 0: primário. Backups sempre devem ocorrer na réplica primária.<br /><br /> 1: somente secundário. A execução de backups em uma réplica secundária é preferível.<br /><br /> 2: preferir secundário. A execução de backups em uma réplica secundária é preferível, mas a execução de backups na réplica primária será aceitável se nenhuma réplica secundária estiver disponível para operações de backup. Esse é o comportamento padrão.<br /><br /> 3: qualquer réplica. Nenhuma preferência sobre se os backups são executados na réplica primária ou em uma réplica secundária.<br /><br /> <br /><br /> Para obter mais informações, consulte [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar (60)**|Descrição de **automated_backup_preference**, uma das:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Nenhuma|  
|**Versão**|**smallint**|A versão dos metadados do grupo de disponibilidade armazenados no cluster de failover do Windows. Esse número de versão é incrementado quando novos recursos são adicionados.|  
|**basic_features**|**bit**|Especifica se este é um grupo de disponibilidade básico. Para obter mais informações, consulte [Grupos de disponibilidade básicos &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).|  
|**dtc_support**|**bit**|Especifica se o suporte DTC foi habilitado para este grupo de disponibilidade. A opção **DTC_SUPPORT** de **Criar grupo de disponibilidade** controla essa configuração.|  
|**db_failover**|**bit**|Especifica se o grupo de disponibilidade dá suporte a failover para condições de integridade do banco de dados. A opção **DB_FAILOVER** de **Criar grupo de disponibilidade** controla essa configuração.|  
|**is_distributed**|**bit**|Especifica se este é um grupo de disponibilidade distribuído. Para obter mais informações, veja [Grupos de disponibilidade distribuídos e &#40;Grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).|  
  
## <a name="failure-condition-level--values"></a>Valores de nível de condição de falha  
 A tabela a seguir descreve os possíveis níveis de condição de falha para a coluna **failure_condition_level** .  
  
|Valor|Condição de falha|  
|-----------|-----------------------|  
|1|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> <br /><br /> -O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço está inoperante.<br /><br /> -A concessão do grupo de disponibilidade para se conectar ao cluster de failover do WSFC expira porque nenhuma confirmação é recebida da instância do servidor. Para obter mais informações, veja [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).|  
|2|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> <br /><br /> -A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não se conecta ao cluster e o limite de **health_check_timeout** especificado pelo usuário do grupo de disponibilidade foi excedido.<br /><br /> -A réplica de disponibilidade está em estado de falha.|  
|3|Especifica que um failover automático deve ser iniciado em erros internos críticos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como spinlocks órfãos, violações do acesso de gravação graves ou muito descarte.<br /><br /> Esse é o valor padrão.|  
|4|Especifica que um failover automático deve ser iniciado em caso de erros internos moderados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como uma condição de memória insuficiente persistente no pool de recursos interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que um failover automático deve ser iniciado em qualquer condição de falha qualificada, incluindo:<br /><br /> <br /><br /> -Esgotamento do trabalho do mecanismo do SQL-threads.<br /><br /> -Detecção de um deadlock não resolvivel.|  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION na instância de servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
