---
title: resource_governor_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d24885b194f8614e393c7529fac0dc34eb3e15fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857210"
---
# <a name="sysresourcegovernorworkloadgroups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a configuração armazenada do grupo de cargas de trabalho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada grupo de carga de trabalho pode assinar apenas um pool de recursos.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|ID exclusivo do grupo de carga de trabalho. Não permite valor nulo.|  
|nome|**sysname**|Nome do grupo de carga de trabalho. Não permite valor nulo.|  
|importance|**sysname**|**Observação:** importância só se aplica a grupos de carga de trabalho no mesmo pool de recursos.<br /><br /> É a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é uma das seguintes opções, com MEDIUM sendo o padrão: baixa, média, alta.<br /><br /> Não permite valor nulo.|  
|request_max_memory_grant_percent|**int**|Porcentagem máxima de concessão de memória para uma única solicitação. O valor padrão é 25. Não permite valor nulo.<br /><br /> **Observação:** se essa configuração for maior que 50%, consultas maiores serão executadas uma por vez. Por isso, haverá maior risco de ser exibido o erro de falta de memória enquanto a consulta estiver sendo executada.|  
|request_max_cpu_time_sec|**int**|Limite máximo de uso da CPU, em segundos, para uma única solicitação. O valor padrão, 0, não especifica nenhum limite. Não permite valor nulo.<br /><br /> **Observação:** para obter mais informações, consulte [limite de CPU excedido classe de evento](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|request_memory_grant_timeout_sec|**int**|Tempo limite de concessão de memória, em segundos, para uma única solicitação. O valor padrão, 0, usa um cálculo interno baseado em custo de consulta. Não permite valor nulo.|  
|max_dop|**int**|Grau máximo de paralelismo para o grupo de carga de trabalho. O valor padrão, 0, usa configurações globais. Não permite valor nulo.<br /><br /> **Nó:** essa configuração substituirá a opção de consulta **maxdop**.|  
|group_max_requests|**int**|Número máximo de solicitações simultâneas. O valor padrão, 0, não especifica nenhum limite. Não permite valor nulo.|  
|pool_id|**int**|ID do pool de recursos utilizado por este grupo de carga de trabalho.|  
|external_pool_id|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do pool de recursos externos que usa esse grupo de carga de trabalho.|  
  
## <a name="remarks"></a>Comentários  
 A exibição do catálogo exibe os metadados armazenados. Para verificar a configuração na memória, use a exibição de gerenciamento dinâmico correspondente [DM resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 A configuração na memória e armazenada poderá ser diferente se a configuração do Administrador de recursos tiver sido alterada, mas a instrução ALTER RESOURCE GOVERNOR RECONFIGURE não tiver sido aplicada.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION para exibir conteúdo e a permissão CONTROL SERVER para alterar conteúdo.  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo do administrador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
