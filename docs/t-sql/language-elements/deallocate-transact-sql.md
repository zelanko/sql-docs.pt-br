---
title: DEALLOCATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DEALLOCATE
- DEALLOCATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], cursors
- DEALLOCATE statement
- deallocations [SQL Server]
- deleting cursor references
- removing cursor references
ms.assetid: c75cf73d-0268-4c57-973d-b8a84ff801fa
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e0721c0e12c512c437d3ddae2306eff661ee9ae
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634994"
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove uma referência de cursor. Quando a última referência de cursor é desalocada, as estruturas de dados que compõem o cursor são liberadas pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor_name*  
 É o nome de um cursor já declarado. Se houver um cursor global e um cursor local com *cursor_name* como seus nomes, o *cursor_name* se referirá ao cursor global se `GLOBAL` for especificado e ao cursor local se `GLOBAL` não for especificado.  
  
 @*cursor_variable_name*  
 É o nome de uma variável de **cursor**. @*cursor_variable_name* precisa ser do tipo **cursor**.  
  
## <a name="remarks"></a>Comentários  
As instruções que operam em cursores usam um nome de cursor ou uma variável de cursor para se referir ao cursor. `DEALLOCATE` remove a associação entre um cursor e o nome de cursor ou variável de cursor. Se um nome ou uma variável forem os últimos a referenciarem o cursor, ele será desalocado e qualquer recurso usado por ele será liberado. Os bloqueios de rolagem usados para proteger o isolamento de buscas são liberados em `DEALLOCATE`. Os bloqueios de transação usados para proteger atualizações, incluindo atualizações posicionadas feitas através do cursor, são mantidos até o fim da transação.  
  
A instrução `DECLARE CURSOR` aloca e associa um cursor a um nome de cursor.  
  
```sql  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
Depois que um nome de cursor é associado a um cursor, o nome não pode ser usado para outro cursor do mesmo escopo (global ou local) até que este tenha sido desalocado.  
  
 Uma variável de cursor é associada a um cursor usando um destes dois métodos:  
  
-   Pelo nome usando uma instrução `SET` que define um cursor como uma variável de cursor.  
  
    ```sql  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   Um cursor também pode ser criado e associado a uma variável sem ter um nome de cursor definido.  
  
    ```sql  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 Uma instrução `DEALLOCATE <@cursor_variable_name>` remove somente a referência da variável nomeada ao cursor. A variável não é desalocada até que saia do escopo no fim do lote, procedimento armazenado ou gatilho. Depois de uma instrução `DEALLOCATE <@cursor_variable_name>`, a variável pode ser associada a outro cursor usando a instrução SET.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
  
DEALLOCATE @MyCursor;  
  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesTerritory;  
GO  
```  
  
Uma variável de cursor não precisa ser desalocada explicitamente. A variável é implicitamente desalocada quando sai de escopo.  
  
## <a name="permissions"></a>Permissões  
 As permissões para `DEALLOCATE` são padronizadas para qualquer usuário válido.  
  
## <a name="examples"></a>Exemplos  
 O script a seguir mostra como os cursores persistem até o último nome ou até a variável que os referenciam ser desalocada.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create and open a global named cursor that  
-- is visible outside the batch.  
DECLARE abc CURSOR GLOBAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
OPEN abc;  
GO  
-- Reference the named cursor with a cursor variable.  
DECLARE @MyCrsrRef1 CURSOR;  
SET @MyCrsrRef1 = abc;  
-- Now deallocate the cursor reference.  
DEALLOCATE @MyCrsrRef1;  
-- Cursor abc still exists.  
FETCH NEXT FROM abc;  
GO  
-- Reference the named cursor again.  
DECLARE @MyCrsrRef2 CURSOR;  
SET @MyCrsrRef2 = abc;  
-- Now deallocate cursor name abc.  
DEALLOCATE abc;  
-- Cursor still exists, referenced by @MyCrsrRef2.  
FETCH NEXT FROM @MyCrsrRef2;  
-- Cursor finally is deallocated when last referencing  
-- variable goes out of scope at the end of the batch.  
GO  
-- Create an unnamed cursor.  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
SELECT * FROM Sales.SalesTerritory;  
-- The following statement deallocates the cursor  
-- because no other variables reference it.  
DEALLOCATE @MyCursor;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
