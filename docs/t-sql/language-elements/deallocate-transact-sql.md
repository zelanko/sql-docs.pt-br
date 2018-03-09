---
title: DEALLOCATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fb05fdd9da2f4f724976092bf027f5dde5edd412
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove uma referência de cursor. Quando a última referência de cursor é desalocada, as estruturas de dados que compõem o cursor são liberadas por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor_name*  
 É o nome de um cursor já declarado. Se uma global e um cursor local existirem com *cursor_name* como seu nome, *cursor_name* refere-se ao cursor global se GLOBAL for especificado e ao cursor local se GLOBAL não for especificado.  
  
 @*cursor_variable_name*  
 É o nome de um **cursor** variável. @*cursor_variable_name* deve ser do tipo **cursor**.  
  
## <a name="remarks"></a>Remarks  
 As instruções que operam em cursores usam um nome de cursor ou uma variável de cursor para se referir ao cursor. DEALLOCATE remove a associação entre um cursor e o nome de cursor ou variável de cursor. Se um nome ou uma variável forem os últimos a referenciarem o cursor, ele será desalocado e qualquer recurso usado por ele será liberado. Os bloqueios de rolagem usados para proteger o isolamento de buscas são liberado em DEALLOCATE. Os bloqueios de transação usados para proteger atualizações, incluindo atualizações posicionadas feitas através do cursor, são mantidos até o fim da transação.  
  
 A instrução DECLARE CURSOR aloca e associa um cursor a um nome de cursor.  
  
```  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
 Depois que um nome de cursor é associado a um cursor, o nome não pode ser usado para outro cursor do mesmo escopo (GLOBAL ou LOCAL) até que este tenha sido desalocado.  
  
 Uma variável de cursor é associada a um cursor usando um destes dois métodos:  
  
-   Pelo nome usando uma instrução SET que define um cursor como uma variável de cursor.  
  
    ```  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   Um cursor também pode ser criado e associado a uma variável sem ter um nome de cursor definido.  
  
    ```  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 Um DEALLOCATE @*cursor_variable_name* instrução remove somente a referência da variável nomeada como o cursor. A variável não é desalocada até que saia do escopo no fim do lote, procedimento armazenado ou gatilho. Após um DEALLOCATE @*cursor_variable_name* instrução, a variável pode ser associado com outro cursor usando a instrução SET.  
  
```  
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
 As permissões DEALLOCATE assumem como padrão qualquer usuário válido.  
  
## <a name="examples"></a>Exemplos  
 O script a seguir mostra como os cursores persistem até o último nome ou até a variável que os referenciam ser desalocada.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
