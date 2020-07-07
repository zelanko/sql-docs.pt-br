---
title: sys. dm_tran_session_transactions (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb4c1742ed3b32a20d0026dad914a0fc7c90b6ea
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000242"
---
# <a name="sysdm_tran_session_transactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna informações de correlação de transações associadas e sessões.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_tran_session_transactions**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**int**|ID da sessão na qual a transação está sendo executada.|  
|transaction_id|**bigint**|ID da transação.|  
|transaction_descriptor|**binário (8)**|Identificador de transação usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao se comunicar com o driver do cliente.|  
|enlist_count|**int**|Número de solicitações ativas na sessão que trabalha na transação.|  
|is_user_transaction|**bit**|1 = a transação foi iniciada por uma solicitação de usuário.<br /><br /> 0 = Transação de sistema.|  
|is_local|**bit**|1 = Transação local.<br /><br /> 0 = Transação distribuída ou uma transação de sessão associada inscrita.|  
|is_enlisted|**bit**|1 = Transação distribuída inscrita<br /><br /> 0 = Não é uma transação distribuída inscrita|  
|is_bound|**bit**|1 = A transação está ativa na sessão por meio de sessões associadas.<br /><br /> 0 = A transação não está ativa na sessão por meio de sessões associadas.|  
|open_transaction_count||O número de transações abertas para cada sessão.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="remarks"></a>Comentários  
 Por sessões associadas e transações distribuídas, é possível executar uma transação em mais de uma sessão. Nesse caso, sys.dm_tran_session_transactions exibirá várias linhas para o mesmo transaction_id, uma para cada sessão em que a transação está sendo executada.  
  
 Ao executar várias solicitações no modo de confirmação automática, usando conjuntos de resultados ativos múltiplos (MARS), é possível ter mais de uma transação ativa em uma única sessão. Nesse caso, sys.dm_tran_session_transactions exibirá várias linhas para o mesmo session_id, uma para cada transação em execução na sessão.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


