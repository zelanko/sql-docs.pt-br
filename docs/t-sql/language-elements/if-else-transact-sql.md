---
title: IF...ELSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IF_TSQL
- IF
dev_langs:
- TSQL
helpviewer_keywords:
- IF...ELSE keyword
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 676c881f-dee1-417a-bc51-55da62398e81
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b0b19216ce352256355da9b2f0c458f49c036773
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075067"
---
# <a name="ifelse-transact-sql"></a>IF...ELSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Impõe condições na execução de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que segue uma palavra-chave IF e sua condição será executada se a condição for satisfeita: a expressão Booleana retorna TRUE. A palavra-chave opcional ELSE introduz outra instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que será executada quando a condição IF não for atendida: a expressão Booliana retorna FALSE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Boolean_expression*  
 É uma expressão que retorna TRUE ou FALSE. Se a expressão booliana contiver uma instrução SELECT, a instrução SELECT deverá ser incluída entre parênteses.  
  
 { *sql_statement*| *statement_block* }  
 É qualquer instrução ou agrupamento de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], conforme definido por meio de um bloco de instruções. A menos que um bloco de instruções seja usado, a condição IF ou ELSE poderá afetar o desempenho de somente uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Para definir um bloco de instruções, use as palavras-chave BEGIN e END de controle de fluxo.  
  
## <a name="remarks"></a>Remarks  
 Uma construção IF...ELSE pode ser usada em lotes, em procedimentos armazenados e em consultas ad hoc. Quando essa construção é usada em um procedimento armazenado, ela normalmente é usada para testar a existência de algum parâmetro.  
  
 Os testes IF podem ser aninhados depois de outro IF ou seguindo um ELSE. O limite do número de níveis aninhados depende da memória disponível.  
  
## <a name="example"></a>Exemplo  
  
```  
IF DATENAME(weekday, GETDATE()) IN (N'Saturday', N'Sunday')
       SELECT 'Weekend';
ELSE 
       SELECT 'Weekday';
```  
  
 Para obter mais exemplos, confira [ELSE &#40;IF...ELSE&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir usa `IF...ELSE` para determinar qual das duas respostas será mostrada ao usuário, com base no peso de um item na tabela `DimProduct`.  
  
```  
-- Uses AdventureWorksDW  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct 
                  WHERE ProductKey = @productKey)   
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is too heavy to ship and is only available for pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
ELSE  
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is available for shipping or pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Control-of-Flow Language &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md) [Linguagem de controle de fluxo (Transact-SQL)] [ELSE &#40;IF...ELSE&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md) 
  
  



