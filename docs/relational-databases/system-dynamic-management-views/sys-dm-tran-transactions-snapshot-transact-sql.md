---
title: sys. dm_tran_transactions_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b91ac554186c37b2e074dd3faded49a01259222e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262694"
---
# <a name="sysdm_tran_transactions_snapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma tabela virtual para a **sequence_number** de transações que estão ativas quando cada transação de instantâneo é iniciada. A informações retornadas por esta exibição podem lhe ser úteis para fazer o seguinte:  
  
-   Encontrar o número de transações de instantâneo ativas no momento.  
  
-   Identificar modificações de dados ignoradas por uma transação de instantâneo particular. As modificações de dados de uma transação que está ativa quando um instantâneo de transação se inicia serão ignoradas por ele, mesmo depois de a transação ser confirmada.  
  
 Por exemplo, considere a seguinte saída de **Sys. dm_tran_transactions_snapshot**:  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 A coluna `transaction_sequence_num` identifica o número de sequência de transação (XSN) das transações de instantâneo atuais. A saída mostra dois: `59` e `60`. A coluna `snapshot_sequence_num` identifica o número de sequência de transação das transações ativas quando cada transação de instantâneo se inicia.  
  
 A saída mostra que transação de instantâneo XSN-59 se inicia enquanto duas transações ativas, XSN-57 e XSN-58, estiverem em execução. Se XSN-57 ou XSN-58 fizerem modificações de dados, XSN-59 ignorará as mudanças e usará o controle de versão de linha para manter uma exibição transacionalmente consistente do banco de dados.  
  
 A transação de instantâneo XSN-60 ignora modificações de dados feitas pelo XSN-57 e XSN-58 e, igualmente, pelo XSN 59.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dm_tran_transactions_snapshot  
```  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Número de sequência de transação (XSN) de um instantâneo de transação.|  
|**snapshot_id**|**int**|ID de instantâneo para cada instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] iniciada com leitura confirmada, usando controle de versão de linha. Este valor é usado para gerar uma exibição consistente transacional do banco de dados que oferece suporte para cada consulta sendo executada com leitura confirmada, usando controle de versão de linha.|  
|**snapshot_sequence_num**|**bigint**|Número de sequência de transação de uma transação que estava ativa quando o instantâneo de transação começou.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
  
## <a name="remarks"></a>Comentários  
 Quando uma transação de instantâneo começa, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] registra todas as transações ativas naquele momento. **Sys. dm_tran_transactions_snapshot** relata essas informações para todas as transações de instantâneo atualmente ativas.  
  
 Cada transação é identificada por um número de sequência de transação atribuído quando no início da transação. As transações começam quando uma instrução BEGIN TRANSACTION ou BEGIN WORK é executada. No entanto, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] nomeia o número de sequência de transação com a execução da primeira instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a acessar dados, depois da instrução BEGIN TRANSACTION ou BEGIN WORK. Os números de sequência de transação são incrementados de um.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

