---
title: sys.DM os_memory_cache_entries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a69088658cf9e76ac52c882872ef0e1eed6500b9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosmemorycacheentries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre todas as entradas em caches no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta exibição para rastrear entradas de cache para os objetos associados. Você também pode usar esta exibição para obter estatísticas sobre entradas de cache.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_cache_entries**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Endereço do cache. Não permite valor nulo.|  
|**name**|**nvarchar(256)**|Nome do cache. Não permite valor nulo.|  
|**type**|**varchar(60)**|Tipo de cache. Não permite valor nulo.|  
|**entry_address**|**varbinary(8)**|Endereço do descritor da entrada de cache. Não permite valor nulo.|  
|**entry_data_address**|**varbinary(8)**|Endereço dos dados de usuário na entrada de cache.<br /><br /> 0x00000000 = Endereço de dados de entrada não está disponível.<br /><br /> Não permite valor nulo.|  
|**in_use_count**|**Int**|Número de usuários simultâneos desta entrada de cache. Não permite valor nulo.|  
|**is_dirty**|**bit**|Indica se a entrada de cache está marcada para remoção. 1 = marcada para remoção. Não permite valor nulo.|  
|**disk_ios_count**|**Int**|Número de E/S incorrido durante a criação dessa entrada. Não permite valor nulo.|  
|**context_switches_count**|**Int**|Número de alternâncias de contexto incorrido durante a criação dessa entrada. Não permite valor nulo.|  
|**original_cost**|**Int**|Custo original da entrada. Esse valor é uma aproximação do número de E/S incorrido, do custo de instrução de CPU e da quantidade de memória consumida pela entrada. Quanto maior o custo, menor a chance de o item ser removido do cache. Não permite valor nulo.|  
|**current_cost**|**Int**|Custo atual da entrada de cache. Este valor é atualizado durante o processo de limpeza de entrada. O custo atual é redefinido com seu valor original na reutilização da entrada. Não permite valor nulo.|  
|**memory_object_address**|**varbinary(8)**|Endereço do objeto de memória associado. Permite valor nulo.|  
|**pages_allocated_count**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Número de páginas de 8 KB para armazenar esta entrada de cache. Não permite valor nulo.|  
|**pages_kb**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Quantidade de memória em quilobytes (KB) usada por essa entrada de cache.  Não permite valor nulo.|  
|**entry_data**|**nvarchar(2048)**|Representação serializada da entrada de cache. Essa informação é dependente do repositório de cache. Permite valor nulo.|  
|**pool_id**|**Int**|**Aplica-se a**: do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do pool de recursos associado à entrada. Permite valor nulo.<br /><br /> não katmai|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões 

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

## <a name="see-also"></a>Consulte também  
 
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


