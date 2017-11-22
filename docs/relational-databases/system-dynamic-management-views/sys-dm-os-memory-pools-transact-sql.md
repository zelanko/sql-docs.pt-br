---
title: sys.DM os_memory_pools (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e0e649688167c772defa308172f3b8a633ab6b7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada repositório de objeto na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar esta exibição para monitorar o uso de memória cache e identificar comportamento ruim de cache  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_memory_pools**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary (8)**|Endereço de memória da entrada que representa o pool de memória. Não permite valor nulo.|  
|**pool_id**|**int**|ID de um pool específico em um conjunto de pools. Não permite valor nulo.|  
|**tipo**|**nvarchar (60)**|Tipo de pool de memória. Não permite valor nulo. Para obter mais informações, consulte [sys.DM os_memory_clerks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**name**|**nvarchar(256)**|Nome atribuído pelo sistema deste objeto de memória. Não permite valor nulo.|  
|**max_free_entries_count**|**bigint**|Número máximo de entradas livres que um pool pode ter. Não permite valor nulo.|  
|**free_entries_count**|**bigint**|Número de entradas livres atualmente no pool. Não permite valor nulo.|  
|**removed_in_all_rounds_count**|**bigint**|Número de entradas removidas do pool desde que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciada. Não permite valor nulo.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.  
  
## <a name="remarks"></a>Comentários  
 Os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] às vezes usam uma estrutura de pool comum para armazenar em cache tipos de dados homogêneos e sem monitoração de estado. A estrutura de pool é mais simples que a estrutura de cache. Todas as entradas nos pools são consideradas iguais. Internamente, os pools são administradores de memória e podem ser usados em locais onde os administradores de memória são usados.  
  
## <a name="see-also"></a>Consulte também  
 
  [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


