---
title: WHILE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WHILE_TSQL
- WHILE
dev_langs: TSQL
helpviewer_keywords:
- statements [SQL Server], repeated executions
- statement blocks [SQL Server]
- repeated statement executions
- nested WHILE loops
- WHILE keyword
ms.assetid: 52dd29ab-25d7-4fd3-a960-ac55c30c9ea9
caps.latest.revision: "40"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 62f346d7a32e6c1aa55e42666ad39f426e1ed8a5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="while-transact-sql"></a>WHILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Define uma condição para a execução repetida de uma instrução ou um bloco de instruções SQL. As instruções serão executadas repetidamente desde que a condição especificada seja verdadeira. A execução de instruções no loop WHILE pode ser controlada internamente ao loop com as palavras-chave BREAK e CONTINUE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK | CONTINUE }  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Boolean_expression*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que retorna **TRUE** ou **FALSE**. Se a expressão booliana contiver uma instrução SELECT, a instrução SELECT deverá ser incluída entre parênteses.  
  
 {*sql_statement* | *statement_block*}  
 É qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou agrupamento de instruções, conforme definido com um bloco de instruções. Para definir um bloco de instruções, use as palavras-chave BEGIN e END de controle de fluxo.  
  
 BREAK  
 Provoca uma saída do loop WHILE mais interno. Todas as instruções que apareçam depois da palavra-chave END, que marca o final do loop, serão executadas.  
  
 CONTINUE  
 Faz com que o loop WHILE seja reiniciado, ignorando todas as instruções depois da palavra-chave CONTINUE.  
  
## <a name="remarks"></a>Remarks  
 Se dois ou mais loops WHILE estiverem aninhados, o BREAK interno será encerrado para o próximo loop mais externo. Todas as instruções após o fim da primeira execução do loop interno e o loop mais externo seguinte serão reiniciadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-break-and-continue-with-nested-ifelse-and-while"></a>A. Usando BREAK e CONTINUE com IF...ELSE e WHILE aninhados  
 No exemplo a seguir, se o preço médio de tabela de um produto for menor que `$300`, o loop `WHILE` dobrará os preços e selecionará o preço máximo. Se o preço máximo for menor ou igual a `$500`, o loop `WHILE` será reiniciado e dobrará novamente os preços. Esse loop continuará dobrando os preços até que o preço máximo seja maior que `$500`; em seguida, sairá do loop `WHILE` e imprimirá uma mensagem.  
  
```  
USE AdventureWorks2012;  
GO  
WHILE (SELECT AVG(ListPrice) FROM Production.Product) < $300  
BEGIN  
   UPDATE Production.Product  
      SET ListPrice = ListPrice * 2  
   SELECT MAX(ListPrice) FROM Production.Product  
   IF (SELECT MAX(ListPrice) FROM Production.Product) > $500  
      BREAK  
   ELSE  
      CONTINUE  
END  
PRINT 'Too much for the market to bear';  
```  
  
### <a name="b-using-while-in-a-cursor"></a>B. Usando WHILE em um cursor  
 O exemplo a seguir usa `@@FETCH_STATUS` para controlar atividades de cursor em um loop `WHILE`.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title   
FROM AdventureWorks2012.HumanResources.Employee  
WHERE JobTitle = 'Marketing Specialist';  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-while-loop"></a>C: simples Loop While  
 No exemplo a seguir, se o preço médio de tabela de um produto for menor que `$300`, o loop `WHILE` dobrará os preços e selecionará o preço máximo. Se o preço máximo for menor ou igual a `$500`, o loop `WHILE` será reiniciado e dobrará novamente os preços. Esse loop continuará dobrando os preços até que o preço máximo seja maior do que `$500`e, em seguida, encerra o `WHILE` loop.  
  
```  
-- Uses AdventureWorks  
  
WHILE ( SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300  
BEGIN  
    UPDATE dbo.DimProduct  
        SET ListPrice = ListPrice * 2;  
    SELECT MAX ( ListPrice) FROM dbo.DimProduct  
    IF ( SELECT MAX (ListPrice) FROM dbo.DimProduct) > $500  
        BREAK;  
END  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Linguagem de controle de fluxo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  


