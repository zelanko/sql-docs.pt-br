---
title: sys.dm_tran_session_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24c91e3965472efec417f5b763338916f17e344b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090526"
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações de correlação de transações associadas e sessões.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_tran_session_transactions**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**int**|ID da sessão na qual a transação está sendo executada.|  
|transaction_id|**bigint**|ID da transação.|  
|transaction_descriptor|**binary(8)**|Identificador de transação usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se comunicar com o driver do cliente.|  
|enlist_count|**int**|Número de solicitações ativas na sessão que trabalha na transação.|  
|is_user_transaction|**bit**|1 = a transação foi iniciada por uma solicitação de usuário.<br /><br /> 0 = Transação de sistema.|  
|is_local|**bit**|1 = Transação local.<br /><br /> 0 = Transação distribuída ou uma transação de sessão associada inscrita.|  
|is_enlisted|**bit**|1 = Transação distribuída inscrita<br /><br /> 0 = Não é uma transação distribuída inscrita|  
|is_bound|**bit**|1 = A transação está ativa na sessão por meio de sessões associadas.<br /><br /> 0 = A transação não está ativa na sessão por meio de sessões associadas.|  
|open_transaction_count||O número de transações abertas para cada sessão.|  
|pdw_node_id|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer a permissão `VIEW DATABASE STATE` no banco de dados.   

## <a name="remarks"></a>Comentários  
 Por sessões associadas e transações distribuídas, é possível executar uma transação em mais de uma sessão. Nesse caso, sys.dm_tran_session_transactions exibirá várias linhas para o mesmo transaction_id, uma para cada sessão em que a transação está sendo executada.  
  
 Ao executar várias solicitações no modo de confirmação automática, usando conjuntos de resultados ativos múltiplos (MARS), é possível ter mais de uma transação ativa em uma única sessão. Nesse caso, sys.dm_tran_session_transactions exibirá várias linhas para o mesmo session_id, uma para cada transação em execução na sessão.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


