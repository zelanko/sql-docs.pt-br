---
title: sys. resource_governor_workload_groups (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fac7eaf3916c773b86b59c6819d577fcc1b8a438
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831402"
---
# <a name="sysresource_governor_workload_groups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a configuração armazenada do grupo de cargas de trabalho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada grupo de carga de trabalho pode assinar apenas um pool de recursos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|group_id|**int**|ID exclusivo do grupo de carga de trabalho. Não permite valor nulo.|  
|Nome|**sysname**|Nome do grupo de carga de trabalho. Não permite valor nulo.|  
|importance|**sysname**|**Observação:** A importância se aplica somente a grupos de carga de trabalho no mesmo pool de recursos.<br /><br /> É a importância relativa de uma solicitação no grupo de carga de trabalho. A importância é um dos seguintes, sendo que médio é o padrão: baixo, médio, alto.<br /><br /> Não permite valor nulo.|  
|request_max_memory_grant_percent|**int**|Porcentagem máxima de concessão de memória para uma única solicitação. O valor padrão é 25. Não permite valor nulo.<br /><br /> **Observação:** Se essa configuração for maior que 50 por cento, as consultas grandes serão executadas uma de cada vez. Por isso, haverá maior risco de ser exibido o erro de falta de memória enquanto a consulta estiver sendo executada.|  
|request_max_cpu_time_sec|**int**|Limite máximo de uso da CPU, em segundos, para uma única solicitação. O valor padrão, 0, não especifica nenhum limite. Não permite valor nulo.<br /><br /> **Observação:** Para obter mais informações, consulte [classe de evento limite de CPU excedido](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|request_memory_grant_timeout_sec|**int**|Tempo limite de concessão de memória, em segundos, para uma única solicitação. O valor padrão, 0, usa um cálculo interno baseado em custo de consulta. Não permite valor nulo.|  
|max_dop|**int**|Grau máximo de paralelismo para o grupo de carga de trabalho. O valor padrão, 0, usa configurações globais. Não permite valor nulo.<br /><br /> **Nó:** Essa configuração substituirá a opção de consulta **MAXDOP**.|  
|group_max_requests|**int**|Número máximo de solicitações simultâneas. O valor padrão, 0, não especifica nenhum limite. Não permite valor nulo.|  
|pool_id|**int**|ID do pool de recursos utilizado por este grupo de carga de trabalho.|  
|external_pool_id|**int**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.<br /><br /> ID do pool de recursos externos que esse grupo de carga de trabalho usa.|  
  
## <a name="remarks"></a>Comentários  
 A exibição do catálogo exibe os metadados armazenados. Para ver a configuração na memória, use a exibição de gerenciamento dinâmico correspondente, [Sys. dm_resource_governor_workload_groups &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 A configuração na memória e armazenada poderá ser diferente se a configuração do Administrador de recursos tiver sido alterada, mas a instrução ALTER RESOURCE GOVERNOR RECONFIGURE não tiver sido aplicada.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW ANY DEFINITION para exibir conteúdo e a permissão CONTROL SERVER para alterar conteúdo.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Resource Governor exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
