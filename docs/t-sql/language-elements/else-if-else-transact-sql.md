---
title: ELSE (IF... ELSE) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18adc4f441fddecdb3cd96c2a253268a16daea46
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="else-ifelse-transact-sql"></a>ELSE (IF...ELSE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Impõe condições na execução de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. O [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução (*sql_statement*) seguir o *Boolean_expression*será executada se a *Boolean_expression* for avaliada como TRUE. A palavra-chave ELSE opcional é uma alternativa [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução é executada quando *Boolean_expression* é avaliada como FALSE ou NULL.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Boolean_expression*  
 É uma expressão que retorna TRUE ou FALSE. Se o *Boolean_expression* contém uma instrução SELECT, a instrução SELECT deve ser colocada entre parênteses.  
  
 { *sql_statement* | *statement_block* }  
 É qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou agrupamento de instruções válido, conforme definido com um bloco de instruções. Para definir um bloco de instruções (lote), use as palavras-chave BEGIN e END da linguagem de controle de fluxo. Embora todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] sejam válidas em um bloco BEGIN...END, certas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] não devem ser agrupadas no mesmo lote (bloco de instrução).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. Usando uma expressão booliana simples  
 O exemplo a seguir tem uma expressão booliana simples (`1=1`) que é true e, portanto, imprime a primeira instrução.  
  
```  
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 O exemplo a seguir tem uma expressão booliana simples (`1=2`) que é false e, portanto, imprime a segunda instrução.  
  
```  
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>B. Usando uma consulta como parte de uma expressão booliana  
 O exemplo a seguir executa uma consulta como parte da expressão booliana. Como há 10 bicicletas na tabela `Product` que atendem à cláusula `WHERE`, a primeira instrução de impressão será executada. Altere `> 5` para `> 15` para saber como a segunda parte da instrução poderia ser executada.  
  
```  
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. Usando um bloco de instrução  
 O exemplo a seguir executa uma consulta como parte da expressão booliana e depois executa blocos de instrução ligeiramente diferentes com base no resultado da expressão booliana. Cada bloco de instrução começa com `BEGIN` e termina com `END`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight decimal(8,2), @BikeCount int  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS varchar(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. Usando instruções IF...ELSE aninhadas  
 O exemplo a seguir mostra como uma instrução IF... Instrução ELSE pode ser aninhada em outra. Defina a variável `@Number` como `5`, `50` e `500` para testar cada instrução.  
  
```  
DECLARE @Number int;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E: usando uma consulta como parte de uma expressão booliana  
 O exemplo a seguir usa `IF…ELSE` determinar qual das duas respostas para mostrar ao usuário, com base no peso de um item de `DimProduct` tabela.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Linguagem de controle de fluxo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  



