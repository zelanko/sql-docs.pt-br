---
title: sys.dm_io_pending_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e35ff23a420421bfd58f70d9309013c9193db2c1
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmiopendingiorequests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Retorna uma linha para cada solicitação de E/S pendente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_io_pending_io_requests**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|Endereço de memória da solicitação de E/S. Não permite valor nulo.|  
|**io_type**|**varchar(7)**|Tipo de solicitação de E/S pendente. Não permite valor nulo.|  
|**io_pending**|**Int**|Indica se a solicitação de E/S está pendente ou foi concluída pelo Windows. Uma solicitação de E/S ainda pode ficar pendente mesmo que o Windows a conclua, caso o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não execute uma opção de contexto que processe a solicitação de E/S e a remova da lista. Não permite valor nulo.|  
|**io_completion_routine_address**|**varbinary(8)**|Função interna a ser chamada quando a solicitação de E/S é concluída. Permite valor nulo.|  
|**io_user_data_address**|**varbinary(8)**|Somente para uso interno. Permite valor nulo.|  
|**scheduler_address**|**varbinary(8)**|Agendador no qual esta solicitação de E/S foi emitida. A solicitação de E/S será exibida na lista de E/S pendente do agendador. Para obter mais informações, consulte [sys.DM os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). Não permite valor nulo.|  
|**io_handle**|**varbinary(8)**|Identificador de arquivo do arquivo usado na solicitação de E/S. Permite valor nulo.|  
|**io_offset**|**bigint**|Deslocamento da solicitação de E/S. Não permite valor nulo.|  
|**io_pending_ms_ticks**|**Int**|Somente para uso interno. Não permite valor nulo.|  
|**pdw_node_id**|**Int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Eu O exibições de gerenciamento dinâmico e funções relacionadas a &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


