---
title: EXCEPT e INTERSECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9e0f46e098ec0944577738332a38e08384a2579
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121770"
---
# <a name="set-operators---except-and-intersect-transact-sql"></a>Operadores de conjunto – EXCEPT e INTERSECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna linhas distintas comparando os resultados de duas consultas.  
  
EXCETO retorna linhas distintas da consulta de entrada à esquerda que não são produzidas pela consulta de entrada à direita.  
 
INTERSECT retorna linhas distintas que são produzidas pelo operador das consultas de entrada à esquerda e à direita.  
  
Para combinar os conjuntos de resultados de duas consultas que usam EXCEPT ou INTERSECT, as regras básicas são:  
  
-   O número e a ordem das colunas devem ser iguais em todas as consultas.  
  
-   Os tipos de dados devem ser compatíveis.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>Argumentos  
\<_query\_specification_> | ( \<_query\_expression_> )  
É uma especificação ou expressão de consulta que retorna dados a serem comparados com os dados de outra especificação ou expressão de consulta. As definições das colunas que fazem parte de uma operação EXCEPT ou INTERSECT não precisam ser iguais. Porém, elas devem ser semelhantes na conversão implícita. Quando os tipos de dados diferem, as regras para [precedência de tipo de dados](../../t-sql/data-types/data-type-precedence-transact-sql.md) determinam o tipo de dados que é executado para comparação.  
  
O resultado se baseia nas mesmas regras para combinar expressões quando os tipos são iguais, mas diferem em precisão, escala ou tamanho. Para obter mais informações, consulte [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
A especificação ou expressão de consulta não pode retornar colunas **xml**, **text**, **ntext**, **image** ou colunas de tipo de dado CLR definido pelo usuário não binárias, pois esses tipos de dados não são comparáveis.  
  
EXCEPT  
Retorna qualquer valor distinto da consulta à esquerda do operador EXCEPT. Esses valores são retornados desde que a consulta à direita não retorne esse valores também.  
  
INTERSECT  
Retorna qualquer valor distinto retornado pela consulta à esquerda e à direita do operador INTERSECT.  
  
## <a name="remarks"></a>Remarks  
Os tipos de dados de colunas comparáveis são retornados pelas consultas à esquerda e à direita dos operadores EXCEPT ou INTERSECT. Esses tipos de dados podem incluir tipos de dados de caractere com ordenações diferentes. Quando isso acontece, a comparação necessária é executada de acordo com as regras de [precedência de ordenação](../../t-sql/statements/collation-precedence-transact-sql.md). Se você não puder executar essa conversão, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] retornará um erro.  
  
Ao comparar valores de colunas para determinar linhas DISTINTAS, dois valores NULL são considerados iguais.  
  
EXCEPT e INTERSECT retornam os nomes de coluna do conjunto de resultados que são iguais aos nomes de coluna retornados pela consulta do lado esquerdo do operador.  
  
Os nomes ou aliases de coluna nas cláusulas ORDER BY devem referenciar nomes de coluna retornados pela consulta à esquerda.  
  
A nulidade de qualquer coluna do conjunto de resultados retornada por EXCEPT ou INTERSECT é igual à nulidade da coluna correspondente que é retornada pela consulta do lado esquerdo do operador.  
  
Se EXCEPT ou INTERSECT forem usados com outros operadores em uma expressão, eles serão avaliados no contexto da seguinte precedência:  
  
1.  Expressões entre parênteses  
  
2.  O operador INTERSECT  
  
3.  EXCEPT e UNION avaliados da esquerda para a direita com base em sua posição na expressão  
  
Você pode usar EXCEPT ou INTERSECT para comparar mais de dois conjuntos de consultas. Quando isso é feito, a conversão de tipo de dados é determinada pela comparação de duas consultas por vez e segue as regras de avaliação de expressão mencionadas anteriormente.  
  
EXCEPT e INTERSECT não podem ser usados em definições de exibição particionadas distribuídas e notificações de consulta.  
 
EXCEPT e INETERSECT podem ser usados em consultas distribuídas, mas são executados somente no servidor local e não são enviados ao servidor vinculado. Desse modo, o uso de EXCEPT e INTERSECT em consultas distribuídas pode afetar desempenho.  
  
Você pode usar cursores estáticos e somente de avanço rápido no conjunto de resultados quando eles são usados com uma operação EXCEPT ou INTERSECT. Também é possível usar um cursor dinâmico ou orientado ao conjunto de chaves com uma operação EXCEPT ou INTERSECT. Quando você faz isso, o cursor do conjunto de resultados da operação é convertido em um cursor estático.  
  
Quando uma operação EXCEPT é exibida usando o recurso Plano de Execução Gráfico no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a operação é exibida como uma [left anti semi join](../../relational-databases/showplan-logical-and-physical-operators-reference.md), e uma operação INTERSECT é exibida como uma [left semi join](../../relational-databases/showplan-logical-and-physical-operators-reference.md).  
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir mostram o uso dos operadores `INTERSECT` e `EXCEPT`. A primeira consulta retorna todos os valores da tabela `Production.Product` para comparar com os resultados de `INTERSECT` e `EXCEPT`.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
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