---
title: DM tran_current_transaction (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_current_transaction
- sys.dm_tran_current_transaction_TSQL
- dm_tran_current_transaction_TSQL
- dm_tran_current_transaction
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_current_transaction dynamic management view
ms.assetid: 75d5697d-b390-4963-99b8-fa0b4244a40c
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a6ad21884497725d9aadd07f1b681eaef76355c0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532996"
---
# <a name="sysdmtrancurrenttransaction-transact-sql"></a>sys.dm_tran_current_transaction (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma única linha que exibe informações do estado da transação na sessão atual.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_tran_current_transaction**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_tran_current_transaction  
```  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|ID de transação do instantâneo atual.|  
|**transaction_sequence_num**|**bigint**|Número de sequência da transação que gera a versão de registro.|  
|**transaction_is_snapshot**|**bit**|Estado de isolamento de instantâneo. Este valor será 1 se a transação for iniciada no isolamento de instantâneo. Caso contrário, o valor será 0.|  
|**first_snapshot_sequence_num**|**bigint**|Número de sequência de transação mais baixo das transações que estavam ativas quando o instantâneo foi feito. Em execução, uma transação de instantâneo faz um instantâneo de todas as transações ativas naquele momento. No caso de transações não instantâneo, esta coluna mostra 0.|  
|**last_transaction_sequence_num**|**bigint**|Número de sequência global. Este valor representa o último número de sequência de transação que foi gerado pelo sistema.|  
|**first_useful_sequence_num**|**bigint**|Número de sequência global. Este valor representa o número de sequência de transação mais antigo da transação que tem versões de linha que devem ser retidas no armazenamento de versões. As versões de linha que foram criadas por transações anteriores podem ser removidas.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa um cenário de teste no qual quatro transações simultâneas, cada uma identificada por um XSN (número de sequência de transação), estão sendo executadas em um banco de dados no qual as opções ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT estão definidas como ON. As seguintes transações estão sendo executadas:  
  
-   XSN-57 é uma operação de atualização sob o isolamento serializável.  
  
-   XSN-58 é o mesmo que XSN-57.  
  
-   XSN-59 é uma operação de seleção em isolamento de instantâneo.  
  
-   XSN-60 é o mesmo que XSN-59.  
  
 A consulta a seguir é executada no escopo de cada transação.  
  
```  
SELECT   
    transaction_id  
   ,transaction_sequence_num  
   ,transaction_is_snapshot  
   ,first_snapshot_sequence_num  
   ,last_transaction_sequence_num  
   ,first_useful_sequence_num  
  FROM sys.dm_tran_current_transaction;  
```  
  
 Aqui está o resultado de XSN-59.  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9387                 59                       1                         
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
57                               61                        
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 A saída mostra que XSN-59 é uma transação de instantâneo que usa XSN-57 como a primeira transação que estava ativa quando XSN-59 foi iniciado. Isso significa que XSN-59 lê dados confirmados por transações com um número de sequência de transação inferior a XSN-57.  
  
 Aqui está o resultado de XSN-57.  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9295                 57                       0  
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
NULL                        61  
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 Como XSN-57 não é uma transação de instantâneo, `first_snapshot_sequence_num` é `NULL`.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


