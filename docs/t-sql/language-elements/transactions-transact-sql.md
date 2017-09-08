---
title: "Transações (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Transactions
- Transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactions [SQL Server]
- transactions [SQL Server], about transactions
- UOW [SQL Server]
- unit of work [SQL Server]
ms.assetid: 1485c375-921a-42af-a871-bb333cc08d3e
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8660d0ac8d6205a94fdab24f41e41bac40a8671e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="transactions-transact-sql"></a>transações (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Uma transação é uma única unidade de trabalho. Se uma transação tiver êxito, todas as modificações de dados feitas durante a transação estarão confirmadas e se tornarão parte permanente do banco de dados. Se uma transação encontrar erros e precisar ser cancelada ou revertida, todas as modificações de dados serão apagadas.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opera nos modos de transação a seguir.  
  
 Transações de confirmação automática  
 Cada instrução individual é uma transação.  
  
 Transações explícitas  
 Cada transação é iniciada explicitamente com a instrução BEGIN TRANSACTION e finalizada explicitamente com uma instrução COMMIT ou ROLLBACK.  
  
 Transações implícitas  
 Uma transação nova é iniciada implicitamente quando a transação anterior é concluída, mas cada transação é explicitamente concluída com uma instrução COMMIT ou ROLLBACK.  
  
 Transações de escopo de lote  
 Aplicável apenas a MARS (Conjuntos de Resultados Ativos Múltiplos), a transação [!INCLUDE[tsql](../../includes/tsql-md.md)] explícita ou implícita iniciada em uma sessão MARS se torna uma transação de escopo de lote. A transação de escopo de lote que não é confirmada ou revertida quando um lote é concluído, será revertida automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece as instruções de transação a seguir.  
  
|||  
|-|-|  
|[TRANSAÇÃO DISTRIBUÍDA DE INÍCIO](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)|[REVERSÃO DE TRANSAÇÃO](../../t-sql/language-elements/rollback-transaction-transact-sql.md)|  
|[COMEÇAR TRANSAÇÃO](../../t-sql/language-elements/begin-transaction-transact-sql.md)|[TRABALHO DE REVERSÃO](../../t-sql/language-elements/rollback-work-transact-sql.md)|  
|[CONFIRMAR TRANSAÇÃO](../../t-sql/language-elements/commit-transaction-transact-sql.md)|[SALVAR A TRANSAÇÃO](../../t-sql/language-elements/save-transaction-transact-sql.md)|  
|[CONFIRMAR O TRABALHO](../../t-sql/language-elements/commit-work-transact-sql.md)||  
  
## <a name="see-also"></a>Consulte também  
 [DEFINIDO IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
