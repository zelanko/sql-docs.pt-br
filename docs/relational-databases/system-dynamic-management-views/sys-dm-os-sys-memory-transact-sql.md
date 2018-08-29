---
title: sys.dm_os_sys_memory (Transact-SQL) | Microsoft Docs
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
- dm_os_sys_memory
- sys.dm_os_sys_memory_TSQL
- sys.dm_os_sys_memory
- dm_os_sys_memory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_memory dynamic management view
ms.assetid: 1ca58814-1caa-44c1-b307-ff0bdcbbef62
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7380f47ae405a7fda1bd30cb464cf60bee737a7
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077079"
---
# <a name="sysdmossysmemory-transact-sql"></a>sys.dm_os_sys_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna informações de memória do sistema operacional.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é limitada pelos e responde às condições de memória externa no nível do sistema operacional e os limites físicos do hardware subjacente. Determinar o estado geral do sistema é uma parte importante da avaliação do uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_sys_memory**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**total_physical_memory_kb**|**bigint**|Tamanho total da memória física disponível para o sistema operacional, em kilobyte (KB).|  
|**available_physical_memory_kb**|**bigint**|Tamanho da memória física disponível, em KB.|  
|**total_page_file_kb**|**bigint**|Tamanho do limite de confirmação informado pelo sistema operacional em KB|  
|**available_page_file_kb**|**bigint**|Quantidade total de arquivo de página não usado, em KB.|  
|**system_cache_kb**|**bigint**|Quantidade total de memória cache do sistema, em KB.|  
|**kernel_paged_pool_kb**|**bigint**|Quantidade total da reserva de memória do kernel paginável, em KB.|  
|**kernel_nonpaged_pool_kb**|**bigint**|Quantidade total da reserva de memória do kernel não paginável, em KB.|  
|**system_high_memory_signal_state**|**bit**|Estado do sistema de notificação do recurso de memória alta. Um valor de 1 indica o sinal de memória alto determinado pelo Windows. Para obter mais informações, consulte [CreateMemoryResourceNotification](http://go.microsoft.com/fwlink/?LinkId=82427) na biblioteca MSDN.|  
|**system_low_memory_signal_state**|**bit**|Estado do sistema de notificação do recurso de memória insuficiente. Um valor de 1 indica que o sinal de memória insuficiente definido pelo Windows. Para obter mais informações, consulte [CreateMemoryResourceNotification](http://go.microsoft.com/fwlink/?LinkId=82427) na biblioteca MSDN.|  
|**system_memory_state_desc**|**nvarchar(256)**|Descrição do estado da memória. Veja a tabela abaixo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
|Condição|Valor|  
|---------------|-----------|  
|system_high_memory_signal_state = 1<br /><br /> e<br /><br /> system_low_memory_signal_state = 0|Memória física disponível está alta|  
|system_high_memory_signal_state = 0<br /><br /> e<br /><br /> system_low_memory_signal_state = 1|Memória física disponível é insuficiente.|  
|system_high_memory_signal_state = 0<br /><br /> e<br /><br /> system_low_memory_signal_state = 0|Uso de memória física é constante|  
|system_high_memory_signal_state = 1<br /><br /> e<br /><br /> system_low_memory_signal_state = 1|Estado de memória físico está em transição.<br /><br /> Os sinais alto e baixo nunca devem ficar acionados ao mesmo tempo. Contudo, mudanças rápidas no nível de sistema operacional podem fazer parecer que ambos os valores estão em um aplicativo de modo de usuário. O aparecimento de ambos os sinais acionados será interpretado como um estado de transição.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


