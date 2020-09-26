---
description: '&#x40;&#x40;ROWCOUNT (Transact-SQL)'
title: '@@ROWCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: e0a85b458990042e524b8e8382e75ce7c4cf27b1
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379957"
---
# <a name="x40x40rowcount-transact-sql"></a>&#x40;&#x40;ROWCOUNT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o número de linhas afetadas pela última instrução. Se o número de linhas for maior que 2 bilhões, use [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
@@ROWCOUNT  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários  
 As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] podem definir o valor de @@ROWCOUNT das seguintes maneiras:  
  
-   Defina @@ROWCOUNT como o número de linhas afetadas ou lidas. As linhas podem ou não ser enviadas ao cliente.  
  
-   Preservar @@ROWCOUNT da execução da instrução anterior.  
  
-   Redefina @@ROWCOUNT como 0, mas não retorne o valor ao cliente.  
  
 Instruções que fazem uma atribuição simples sempre definem o valor de @@ROWCOUNT como 1. Nenhuma linha é enviada ao cliente. Alguns exemplos dessas instruções são: SET @*local_variable*, RETURN, READTEXT e selecione sem instruções de consulta, como SELECT GETDATE() ou SELECT **'***Generic Text***'** .  
  
 As instruções que fazem uma atribuição em uma consulta ou usam RETURN em uma consulta definem o valor de @@ROWCOUNT para o número de linhas afetadas ou lidas pela consulta, por exemplo: SELECT @*local_variable* = c1 FROM t1.  
  
 As instruções DML (linguagem de manipulação de dados) definem o valor de @@ROWCOUNT como o número de linhas afetadas ou lidas pela consulta e retornam esse valor ao cliente. As instruções DML podem não enviar nenhuma linha ao cliente.  
  
 DECLARE CURSOR e FETCH definem o valor @@ROWCOUNT como 1.  
  
 As instruções EXECUTE preservam o @@ROWCOUNT anterior.  
  
 Instruções como USE, SET \<option>, DEALLOCATE CURSOR, CLOSE CURSOR, PRINT, RAISERROR, BEGIN TRANSACTION ou COMMIT TRANSACTION redefinem o valor ROWCOUNT como 0.  
  
 Os procedimentos armazenados compilados nativamente preservam a função @@ROWCOUNT anterior. As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] dentro de procedimentos armazenados compilados nativamente não definem @@ROWCOUNT. Para saber mais, veja [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir executa uma instrução `UPDATE` e usa `@@ROWCOUNT` para detectar se quaisquer linhas foram alteradas.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  
