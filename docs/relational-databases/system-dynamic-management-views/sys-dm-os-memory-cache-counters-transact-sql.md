---
title: sys.DM os_memory_cache_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d1ad3321360a5d982b3ab9110bd56a4409245d0
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmosmemorycachecounters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um instantâneo da integridade de um cache no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **sys.DM os_memory_cache_counters** fornece informações de tempo de execução sobre as entradas de cache alocadas, seu uso e a origem da memória para as entradas de cache.  
  
> **Observação:** chamá-la de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_cache_counters**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Indica o endereço (chave primária) dos contadores associados a um cache específico. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Especifica o nome do cache. Não permite valor nulo.|  
|**type**|**nvarchar(60)**|Indica o tipo de cache que é associado a esta entrada. Não permite valor nulo.|  
|**single_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de uma única página alocada. É a quantidade de memória alocada usando o alocador de uma única página. Faz referência a páginas de 8 KB usadas diretamente do pool de buffers para esse cache. Não permite valor nulo.|  
|**pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica o volume, em quilobytes, da memória alocada no cache. Não permite valor nulo.|  
|**multi_pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de várias páginas alocadas. Esta é a quantidade de memória alocada usando o alocador de várias páginas do nó de memória. Esta memória é alocada fora do pool de buffers e se beneficia do alocador virtual dos nós de memória. Não permite valor nulo.|  
|**pages_in_use_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica o volume, em quilobytes, da memória que está alocada e em uso no cache. Permite valor nulo.  Os valores dos objetos do tipo `USERSTORE_<*>` não são rastreados.  NULL é relatado para eles.|  
|**single_pages_in_use_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de uma única página que está sendo usada. Permite valor nulo. Essas informações não são controladas para objetos do tipo USERSTORE_\<* > e esses valores serão NULL.|  
|**multi_pages_in_use_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Quantidade, em quilobytes, da memória de várias páginas que está sendo usada. É NULLABLE. Essas informações não são controladas para objetos do tipo USERSTORE_\<* >, e esses valores serão NULL.|  
|**entries_count**|**bigint**|Indica o número de entradas no número. Não permite valor nulo.|  
|**entries_in_use_count**|**bigint**|Indica o número de entradas no cache que está sendo usado. Não permite valor nulo.|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões 

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="see-also"></a>Consulte também  
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


