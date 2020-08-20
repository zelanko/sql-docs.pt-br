---
description: sys.dm_os_sys_memory (Transact-SQL)
title: sys. dm_os_sys_memory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 78f02c014874bdce9cf6d1f6e2c27ad0b3fad24d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493614"
---
# <a name="sysdm_os_sys_memory-transact-sql"></a>sys.dm_os_sys_memory (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Retorna informações de memória do sistema operacional.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O  está vinculado, e responde, às condições de memória externa, ao nível do sistema operacional e dos limites físicos do hardware subjacente.  Determinar o estado geral do sistema é uma parte importante da avaliação do uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_sys_memory**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**total_physical_memory_kb**|**bigint**|Tamanho total da memória física disponível para o sistema operacional, em kilobyte (KB).|  
|**available_physical_memory_kb**|**bigint**|Tamanho da memória física disponível, em KB.|  
|**total_page_file_kb**|**bigint**|Tamanho do limite de confirmação informado pelo sistema operacional em KB|  
|**available_page_file_kb**|**bigint**|Quantidade total de arquivo de paginação que não está sendo usada, em KB.|  
|**system_cache_kb**|**bigint**|Quantidade total de memória cache do sistema, em KB.|  
|**kernel_paged_pool_kb**|**bigint**|Quantidade total da reserva de memória do kernel paginável, em KB.|  
|**kernel_nonpaged_pool_kb**|**bigint**|Quantidade total da reserva de memória do kernel não paginável, em KB.|  
|**system_high_memory_signal_state**|**bit**|Estado do sistema de notificação do recurso de memória alta. Um valor de 1 indica o sinal de memória alto determinado pelo Windows. Para obter mais informações, consulte [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) na biblioteca do MSDN.|  
|**system_low_memory_signal_state**|**bit**|Estado do sistema de notificação do recurso de memória insuficiente. Um valor de 1 indica que o sinal de memória insuficiente definido pelo Windows. Para obter mais informações, consulte [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) na biblioteca do MSDN.|  
|**system_memory_state_desc**|**nvarchar(256)**|Descrição do estado da memória. Veja a tabela abaixo.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
|Condição|Valor|  
|---------------|-----------|  
|system_high_memory_signal_state = 1<br /><br /> e<br /><br /> system_low_memory_signal_state = 0|Memória física disponível está alta|  
|system_high_memory_signal_state = 0<br /><br /> e<br /><br /> system_low_memory_signal_state = 1|Memória física disponível é insuficiente.|  
|system_high_memory_signal_state = 0<br /><br /> e<br /><br /> system_low_memory_signal_state = 0|Uso de memória física é constante|  
|system_high_memory_signal_state = 1<br /><br /> e<br /><br /> system_low_memory_signal_state = 1|Estado de memória físico está em transição.<br /><br /> Os sinais alto e baixo nunca devem ficar acionados ao mesmo tempo. Contudo, mudanças rápidas no nível de sistema operacional podem fazer parecer que ambos os valores estão em um aplicativo de modo de usuário. O aparecimento de ambos os sinais acionados será interpretado como um estado de transição.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


