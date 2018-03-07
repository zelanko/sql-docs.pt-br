---
title: '@@TRANCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TRANCOUNT_TSQL'
- '@@TRANCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TRANCOUNT function'
- number of active transactions
- connections [SQL Server], active transactions
- active transactions
ms.assetid: b2638410-e410-4bd0-9b54-90096182b2b6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d9b10f8a7a8f14745765f611bc9ae33f36e7ff0a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40trancount-transact-sql"></a>& #x 40; & #x 40. TRANCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o número de instruções BEGIN TRANSACTION que ocorreram na conexão atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@TRANCOUNT  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 A instrução BEGIN TRANSACTION incrementa@TRANCOUNT em 1. ROLLBACK TRANSACTION reduz @@TRANCOUNT como 0, com exceção de ROLLBACK TRANSACTION *savepoint_name*, que não afeta@TRANCOUNT. COMMIT TRANSACTION ou COMMIT WORK diminui@TRANCOUNT em 1.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-the-effects-of-the-begin-and-commit-statements"></a>A. Mostrando os efeitos das instruções BEGIN e COMMIT  
 O exemplo a seguir mostra o efeito das instruções aninhadas `BEGIN` e `COMMIT` sobre a variável `@@TRANCOUNT`.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The COMMIT statement will decrement the transaction count by 1.  
    COMMIT  
    PRINT @@TRANCOUNT  
COMMIT  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--1  
--0  
```  
  
### <a name="b-showing-the-effects-of-the-begin-and-rollback-statements"></a>B. Mostrando os efeitos das instruções BEGIN e ROLLBACK  
 O exemplo a seguir mostra o efeito das instruções aninhadas `BEGIN TRAN` e `ROLLBACK` sobre a variável `@@TRANCOUNT`.  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The ROLLBACK statement will clear the @@TRANCOUNT variable  
--  to 0 because all active transactions will be rolled back.  
ROLLBACK  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--0  
```  
  
## <a name="see-also"></a>Consulte também  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
