---
title: sys.DM tran_session_transactions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
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
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b247ada006579e642a6ce4c9c4b7b17b153e69c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de correlação de transações associadas e sessões.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_tran_session_transactions**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|ID da sessão na qual a transação está sendo executada.|  
|transaction_id|**bigint**|ID da transação.|  
|transaction_descriptor|**binary (8)**|Identificador de transação usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se comunicar com o driver do cliente.|  
|enlist_count|**int**|Número de solicitações ativas na sessão que trabalha na transação.|  
|is_user_transaction|**bit**|1 = a transação foi iniciada por uma solicitação de usuário.<br /><br /> 0 = Transação de sistema.|  
|is_local|**bit**|1 = Transação local.<br /><br /> 0 = Transação distribuída ou uma transação de sessão associada inscrita.|  
|is_enlisted|**bit**|1 = Transação distribuída inscrita<br /><br /> 0 = Não é uma transação distribuída inscrita|  
|is_bound|**bit**|1 = A transação está ativa na sessão por meio de sessões associadas.<br /><br /> 0 = A transação não está ativa na sessão por meio de sessões associadas.|  
|open_transaction_count||O número de transações abertas para cada sessão.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, requer o `VIEW DATABASE STATE` no banco de dados. Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, requer o **administrador do servidor** ou um **administrador do Active Directory do Azure** conta.  
 
 
  
## <a name="remarks"></a>Comentários  
 Por sessões associadas e transações distribuídas, é possível executar uma transação em mais de uma sessão. Nesse caso, sys.dm_tran_session_transactions exibirá várias linhas para o mesmo transaction_id, uma para cada sessão em que a transação está sendo executada.  
  
 Ao executar várias solicitações no modo de confirmação automática, usando conjuntos de resultados ativos múltiplos (MARS), é possível ter mais de uma transação ativa em uma única sessão. Nesse caso, sys.dm_tran_session_transactions exibirá várias linhas para o mesmo session_id, uma para cada transação em execução na sessão.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


