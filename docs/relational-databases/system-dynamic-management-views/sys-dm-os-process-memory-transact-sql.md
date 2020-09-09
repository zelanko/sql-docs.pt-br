---
description: sys.dm_os_process_memory (Transact-SQL)
title: sys. dm_os_process_memory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4234894d907a383902a00a659e954ccfea2ff74c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539293"
---
# <a name="sysdm_os_process_memory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  A maioria das alocações de memória atribuídas ao espaço de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é controlada por meio de interfaces que permitem o rastreamento e a contabilidade dessas alocações. Porém, poderiam ser executadas alocações de memória no espaço de endereçamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ignora rotinas de administração de memória internas. Os valores são obtidos por chamadas ao sistema operacional de base. Eles não são manipulados por métodos internos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto quando eles se ajustam a alocações de página grandes ou bloqueadas.  
  
 Todos os valores retornados que indicam tamanhos de memória são exibidos em kilobytes (KB). A coluna **total_virtual_address_space_reserved_kb** é uma duplicata de **virtual_memory_in_bytes** de **Sys. dm_os_sys_info**.  
  
 A tabela a seguir fornece um quadro completo do espaço de endereçamento de processos.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_process_memory**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|Indica o conjunto de trabalho do processo em KB, conforme relatado pelo sistema operacional, assim como alocações rastreadas por meio de APIs de página grande. Não permite valor nulo.|  
|**large_page_allocations_kb**|**bigint**|Especifica a memória física alocada com o uso de APIs de página grande. Não permite valor nulo.|  
|**locked_page_allocations_kb**|**bigint**|Especifica páginas de memória bloqueadas na memória. Não permite valor nulo.|  
|**total_virtual_address_space_kb**|**bigint**|Indica o tamanho total da parte de modo de usuário do espaço de endereço virtual. Não permite valor nulo.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indica o espaço total do endereço virtual reservado pelo processo. Não permite valor nulo.|  
|**virtual_address_space_committed_kb**|**bigint**|Indica o espaço de endereço virtual reservado que foi confirmado ou mapeado para páginas físicas. Não permite valor nulo.|  
|**virtual_address_space_available_kb**|**bigint**|Indica o espaço de endereço virtual atualmente livre. Não permite valor nulo.<br /><br /> **Observação:** Regiões livres que são menores do que a granularidade de alocação podem existir. Essas regiões não estão disponível para alocações.|  
|**page_fault_count**|**bigint**|Indica o número de falhas de página incorridas pelo processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não permite valor nulo.|  
|**memory_utilization_percentage**|**int**|Especifica a porcentagem de memória confirmada que está no conjunto de trabalho. Não permite valor nulo.|  
|**available_commit_limit_kb**|**bigint**|Indica a quantidade de memória disponível para ser confirmada pelo processo. Não permite valor nulo.|  
|**process_physical_memory_low**|**bit**|Indica que o processo está respondendo a uma notificação de memória física baixa. Não permite valor nulo.|  
|**process_virtual_memory_low**|**bit**|Indica que uma condição de memória virtual baixa foi detectada. Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessária a permissão VIEW SERVER STATE no servidor.  
  
Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


