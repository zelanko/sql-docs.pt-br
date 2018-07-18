---
title: sys.dm_os_process_memory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5732a15fe8fe2d30f6f9c693e66258c0de4b44d3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37980765"
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  A maioria das alocações de memória atribuídas ao espaço de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é controlada por meio de interfaces que permitem o rastreamento e a contabilidade dessas alocações. Porém, poderiam ser executadas alocações de memória no espaço de endereçamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ignora rotinas de administração de memória internas. Os valores são obtidos por chamadas ao sistema operacional de base. Eles não são manipulados por métodos internos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto nos ajustes para bloqueada ou as alocações de página grande.  
  
 Todos os valores retornados que indicam tamanhos de memória são exibidos em kilobytes (KB). A coluna **total_virtual_address_space_reserved_kb** é uma duplicata de **virtual_memory_in_bytes** da **DM os_sys_info**.  
  
 A tabela a seguir fornece um quadro completo do espaço de endereçamento de processos.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_process_memory**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|Indica o conjunto de trabalho do processo em KB, conforme relatado pelo sistema operacional, assim como alocações rastreadas por meio de APIs de página grande. Não permite valor nulo.|  
|**large_page_allocations_kb**|**bigint**|Especifica a memória física alocada com o uso de APIs de página grande. Não permite valor nulo.|  
|**locked_page_allocations_kb**|**bigint**|Especifica páginas de memória bloqueadas na memória. Não permite valor nulo.|  
|**total_virtual_address_space_kb**|**bigint**|Indica o tamanho total da parte de modo de usuário do espaço de endereço virtual. Não permite valor nulo.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica o espaço total do endereço virtual reservado pelo processo. Não permite valor nulo.|  
|**virtual_address_space_committed_kb**|**bigint**|Indica o espaço de endereço virtual reservado que foi confirmado ou mapeado para páginas físicas. Não permite valor nulo.|  
|**virtual_address_space_available_kb**|**bigint**|Indica o espaço de endereço virtual atualmente livre. Não permite valor nulo.<br /><br /> **Observação:** livre regiões menores que a granularidade de alocação pode existir. Essas regiões não estão disponível para alocações.|  
|**page_fault_count**|**bigint**|Indica o número de falhas de página incorridas pelo processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**memory_utilization_percentage**|**int**|Especifica a porcentagem de memória confirmada que está no conjunto de trabalho. Não permite valor nulo.|  
|**available_commit_limit_kb**|**bigint**|Indica a quantidade de memória disponível para ser confirmada pelo processo. Não permite valor nulo.|  
|**process_physical_memory_low**|**bit**|Indica que o processo está respondendo a uma notificação de memória física baixa. Não permite valor nulo.|  
|**process_virtual_memory_low**|**bit**|Indica que uma condição de memória virtual baixa foi detectada. Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer a permissão VIEW SERVER STATE no servidor.  
  
Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


