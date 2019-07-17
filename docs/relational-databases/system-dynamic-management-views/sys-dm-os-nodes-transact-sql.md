---
title: sys.dm_os_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2b6f88e857ab7fc6300698174914126fb0881f6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265735"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Um componente interno denominado SQLOS cria estruturas de nó que imitam a localidade do processador de hardware. Essas estruturas podem ser alteradas usando [soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) para criar layouts de nó personalizados.  

> [!NOTE]
> Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usará automaticamente o soft-para determinadas configurações de hardware. Para obter mais informações, consulte [Soft-NUMA automático](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).
  
A tabela seguinte fornece informações sobre esses nós.  
  
> [!NOTE]
> Para chamar essa DMV do [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_nodes**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ID do nó.|  
|node_state_desc|**nvarchar(256)**|Descrição do estado do nó. Os valores são exibidos primeiro com os valores mutuamente exclusivos, seguidos pelos valores combinados. Por exemplo:<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />Há quatro valores node_state_desc mutuamente exclusivos. Eles são listados com suas descrições.<br /><ul><li>ONLINE: O nó está online<li>OFFLINE: O nó está offline<li>IDLE: Nó não tem nenhuma solicitação de trabalho pendente e entrou em um estado ocioso.<li>IDLE_READY: Nó não tem nenhuma solicitação de trabalho pendente e está pronto para entrar em um estado ocioso.</li></ul><br />Há três valores combináveis de node_state_desc, listados abaixo, suas descrições.<br /><ul><li>DAC: Este nó é reservado para o [Conexão administrativa dedicada](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).<li>THREAD_RESOURCES_LOW: Nenhum thread novo pode ser criado neste nó devido a uma condição de pouca memória.<li>FREQUENTE ADICIONADOS: Indica os nós foram adicionados em resposta ao evento de CPU de adicionar um ativo.</li></ul>|  
|memory_object_address|**varbinary(8)**|Endereço de objeto de memória associado a esse nó. Relação um para um para [DM os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address.|  
|memory_clerk_address|**varbinary(8)**|Endereço de administrador de memória associado a este nó. Relação um para um para [DM os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address.|  
|io_completion_worker_address|**varbinary(8)**|Endereço de trabalhador atribuído à conclusão de E/S deste nó. Relação um para um para [DM os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address.|  
|memory_node_id|**smallint**|ID do nó de memória ao qual este nó pertence. Relação muitos-para-um com [sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id.|  
|cpu_affinity_mask|**bigint**|Bitmap que identifica as CPUs às quais este nó está associado.|  
|online_scheduler_count|**smallint**|Número de agendadores online que são gerenciados por este nó.|  
|idle_scheduler_count|**smallint**|Número de agendadores online que não têm nenhum trabalhador ativo.|  
|active_worker_count|**int**|Número de trabalhadores que estão ativos em todos os agendadores gerenciados por este nó.|  
|avg_load_balance|**int**|Média do número de trabalhos para cada agendador neste nó.|  
|timer_task_affinity_mask|**bigint**|Bitmap que identifica os agendadores que podem ter trabalhos de timer atribuídos.|  
|permanent_task_affinity_mask|**bigint**|Bitmap que identifica os agendadores que podem ter trabalhos permanentes atribuídos.|  
|resource_monitor_state|**bit**|Cada nó possui um monitor de recursos atribuído. O monitor de recursos pode estar sendo executando ou em estado ocioso. O valor 1 indica que está sendo executado; o valor 0 indica que está em estado ocioso.|  
|online_scheduler_mask|**bigint**|Identifica a máscara de afinidade de processo para este nó.|  
|processor_group|**smallint**|Identifica o grupo de processadores para este nó.|  
|cpu_count |**int** |Número de CPUs disponíveis para este nó. |
|pdw_node_id|**int**|O identificador para o nó que essa distribuição é no.<br /><br /> **Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` permissão no banco de dados. Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e básica, requer a **administrador de servidor** ou uma **administrador do Active Directory do Azure** conta.   

## <a name="see-also"></a>Consulte também    
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
