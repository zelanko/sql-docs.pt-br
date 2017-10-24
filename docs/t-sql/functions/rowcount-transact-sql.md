---
title: '@@ROWCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411dc7eb628ddff52eb2f9426488e05860c9d279
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40rowcount-transact-sql"></a>& #x 40; & #x 40. Número de linhas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o número de linhas afetadas pela última instrução. Se o número de linhas for maior que 2 bilhões, use [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]instruções podem definir o valor de @@ROWCOUNT das seguintes maneiras:  
  
-   Defina@ROWCOUNT para o número de linhas afetadas ou lidas. As linhas podem ou não ser enviadas ao cliente.  
  
-   Preservar@ROWCOUNT da execução da instrução anterior.  
  
-   Redefinir@ROWCOUNT como 0, mas não retornam o valor para o cliente.  
  
 Instruções que fazem uma atribuição simples sempre defina o @@ROWCOUNT valor como 1. Nenhuma linha é enviada ao cliente. Exemplos dessas instruções são: definir*local_variable*, RETURN, READTEXT e select sem consulta instruções como SELECT getDate () ou selecione **'***texto genérico* **'**.  
  
 As instruções que fazem uma atribuição em uma consulta ou usam RETURN em um conjunto de consultas a @@ROWCOUNT valor para o número de linhas afetadas ou lidas pela consulta, por exemplo: selecione*local_variable* = c1 FROM t1.  
  
 Conjunto de instruções de DML (linguagem) de manipulação de dados de @@ROWCOUNT valor para o número de linhas afetadas pela consulta e retornará o valor para o cliente. As instruções DML podem não enviar nenhuma linha ao cliente.  
  
 DECLARE CURSOR e FETCH defina o @@ROWCOUNT valor como 1.  
  
 As instruções EXECUTE preservam o @ anterior@ROWCOUNT.  
  
 Instruções de como usar, defina \<opção >, DEALLOCATE CURSOR, CLOSE CURSOR, BEGIN TRANSACTION ou COMMIT TRANSACTION redefinir o valor de ROWCOUNT para 0.  
  
 Procedimentos armazenados compilados nativamente preservam o @ anterior@ROWCOUNT. [!INCLUDE[tsql](../../includes/tsql-md.md)]as instruções dentro de procedimentos armazenados compilados nativamente não definem@ROWCOUNT. Para obter mais informações, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa uma instrução `UPDATE` e usa `@@ROWCOUNT` para detectar se quaisquer linhas foram alteradas.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [Número de linhas do conjunto de &#40; Transact-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  

