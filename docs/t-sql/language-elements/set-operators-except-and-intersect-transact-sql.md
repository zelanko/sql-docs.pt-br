---
title: EXCEPT e INTERSECT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTERSECT_TSQL
- EXCEPT_TSQL
- INTERSECT
- EXCEPT
dev_langs:
- TSQL
helpviewer_keywords:
- EXCEPT operator [Transact-SQL]
- queries [SQL Server], comparing
- comparing queries
- INTERSECT operator
ms.assetid: b1019300-171a-4a1a-854f-e1e751de3565
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1d8bff51308e9b8dbf02066d56b73829bc1658c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-operators---except-and-intersect-transact-sql"></a>Definir operadores - exceto e INTERSECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna linhas distintas comparando os resultados de duas consultas.  
  
 EXCETO retorna linhas distintas da consulta de entrada à esquerda que não são produzidas pela consulta de entrada à direita.  
  
 INTERSECT retorna linhas distintas que são produzidas pelo operador de consultas de entrada à esquerda e à direita.  
  
 As regras básicas para combinar os conjuntos de resultados de duas consultas que usam EXCEPT ou INTERSECT são as seguintes:  
  
-   O número e a ordem das colunas devem ser iguais em todas as consultas.  
  
-   Os tipos de dados devem ser compatíveis.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>Argumentos  
 \<*query_specification*> | ( \< *query_expression*>)  
 É uma especificação ou expressão de consulta que retorna dados a serem comparados com os dados de outra especificação ou expressão de consulta. As definições das colunas que fazem parte de uma operação EXCEPT ou INTERSECT não precisam ser iguais, mas devem ser compatíveis na conversão implícita. Quando tipos de dados diferem, o tipo que é usado para executar a comparação e retornar resultados é determinado com base nas regras de [precedência de tipo de dados](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
 Quando os tipos são iguais mas diferem em precisão, escala ou extensão, o resultado é determinado com base nas mesmas regras para expressões de combinação. Para obter mais informações, consulte [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 A especificação de consulta ou uma expressão não pode retornar **xml**, **texto**, **ntext**, **imagem**, ou colunas de tipo definido pelo usuário CLR não binários como esses tipos de dados não são comparáveis.  
  
 EXCEPT  
 Retorna qualquer valor distinto da consulta à esquerda do operador EXCEPT que também não são retornados da consulta à direita.  
  
 INTERSECT  
 Retorna qualquer valor distinto retornado pela consulta à esquerda e à direita do operador INTERSECT.  
  
## <a name="remarks"></a>Comentários  
 Quando os tipos de dados de colunas comparáveis retornadas pelas consultas à esquerda e à direita do EXCEPT ou INTERSECT operadores são os tipos de dados de caractere com agrupamentos diferentes, a comparação necessária é executada de acordo com as regras de [ precedência de agrupamento](../../t-sql/statements/collation-precedence-transact-sql.md). Se essa conversão não puder ser executada, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retornará um erro.  
  
 Ao comparar valores de colunas para determinar linhas DISTINTAS, dois valores NULL são considerados iguais.  
  
 Os nomes de colunas do conjunto de resultados retornados por EXCEPT ou INTERSECT são iguais aos retornados pela consulta à esquerda do operador.  
  
 Os nomes ou aliases de coluna nas cláusulas ORDER BY devem referenciar nomes de coluna retornados pela consulta à esquerda.  
  
 A nulabilidade de qualquer coluna do conjunto de resultados retornados por EXCEPT ou INTERSECT é igual à da coluna correspondente retornada pela consulta à esquerda do operador.  
  
 Se EXCEPT ou INTERSECT forem usados junto com outros operadores em uma expressão, eles serão avaliados no contexto da seguinte precedência:  
  
1.  Expressões entre parênteses  
  
2.  O operador INTERSECT  
  
3.  EXCEPT e UNION avaliados da esquerda para a direita com base em sua posição na expressão  
  
 Se EXCEPT ou INTERSECT forem usados para comparar mais de dois conjuntos de consultas, a conversão de tipo de dados é determinada pela comparação de duas consultas por vez e segue as regras de avaliação de expressão mencionadas anteriormente.  
  
 EXCEPT e INTERSECT não podem ser usados em definições de exibição particionadas distribuídas e notificações de consulta.  
  
 EXCEPT e INETERSECT podem ser usados em consultas distribuídas, mas são executados somente no servidor local e não são enviados ao servidor vinculado. Portanto, o uso de EXCEPT e INTERSECT em consultas distribuídas pode afetar desempenho.  
  
 Cursores estáticos e somente de avanço rápido têm suporte total no conjunto de resultados quando são usados com uma operação EXCEPT ou INTERSECT. Se um cursor dinâmico ou controlado por conjunto de chaves for usado com uma operação EXCEPT ou INTERSECT, o cursor do conjunto de resultados da operação será convertido em um cursor estático.  
  
 Quando uma operação EXCEPT é exibida, usando o recurso de plano de execução gráfica no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a operação é exibida como uma [semi antijunção esquerda](../../relational-databases/showplan-logical-and-physical-operators-reference.md), e uma operação INTERSECT é exibida como uma [semijunção à esquerda](../../relational-databases/showplan-logical-and-physical-operators-reference.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar o `INTERSECT` e `EXCEPT` operadores. A primeira consulta retorna todos os valores da tabela `Production.Product` para comparar com os resultados de `INTERSECT` e `EXCEPT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product ;  
--Result: 504 Rows  
```  
  
 A consulta a seguir retorna qualquer valor distinto retornado pela consulta à esquerda e à direita do operador `INTERSECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
INTERSECT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 238 Rows (products that have work orders)  
```  
  
 A consulta a seguir retorna qualquer valor distinto da consulta à esquerda do operador `EXCEPT` que não seja encontrado também na consulta à direita.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
EXCEPT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 266 Rows (products without work orders)  
```  
  
 A consulta a seguir retorna qualquer valor distinto da consulta à esquerda do operador `EXCEPT` que não seja encontrado também na consulta à direita. As tabelas são inversas às do exemplo anterior.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.WorkOrder  
EXCEPT  
SELECT ProductID   
FROM Production.Product ;  
--Result: 0 Rows (work orders without products)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Os exemplos a seguir mostram como usar os operadores `INTERSECT` e `EXCEPT`. A primeira consulta retorna todos os valores da tabela `FactInternetSales` para comparar com os resultados de `INTERSECT` e `EXCEPT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales;  
--Result: 60398 Rows  
```  
  
 A consulta a seguir retorna qualquer valor distinto retornado pela consulta à esquerda e à direita do operador `INTERSECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
INTERSECT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9133 Rows (Sales to customers that are female.)  
```  
  
 A consulta a seguir retorna qualquer valor distinto da consulta à esquerda do operador `EXCEPT` que não seja encontrado também na consulta à direita.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
EXCEPT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9351 Rows (Sales to customers that are not female.)  
```  
  
  


