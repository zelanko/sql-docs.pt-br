---
title: "Expressões (Transact-SQL) | Microsoft Docs"
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
dev_langs: TSQL
helpviewer_keywords:
- Boolean expressions
- expressions [SQL Server], about expressions
- combining expressions
- Transact-SQL expressions
- expressions [SQL Server], combining
- simple expressions [SQL Server]
- complex expressions [SQL Server]
ms.assetid: ee53c5c8-e36c-40f9-8cd1-d933791b98fa
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ab2d66c986bb5b4b34eaf74b4d65dbcb9fcfdd16
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="expressions-transact-sql"></a>Expressões (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  É uma combinação de símbolos e operadores que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] avalia para obter um único valor de dados. Expressões simples podem ser uma única constante, variável, coluna ou função escalar. Os operadores podem ser usados para unir duas ou mais expressões simples em uma expressão complexa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
{ constant | scalar_function | [ table_name. ] column | variable   
    | ( expression ) | ( scalar_subquery )   
    | { unary_operator } expression   
    | expression { binary_operator } expression   
    | ranking_windowed_function | aggregate_windowed_function  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Expression in a SELECT statement  
<expression> ::=   
{  
    constant   
    | scalar_function   
    | column  
    | variable  
    | ( expression  )  
    | { unary_operator } expression   
    | expression { binary_operator } expression   
}  
[ COLLATE Windows_collation_name ]  
  
-- Scalar Expression in a DECLARE, SET, IF…ELSE, or WHILE statement  
<scalar_expression> ::=  
{  
    constant   
    | scalar_function   
    | variable  
    | ( expression  )  
    | (scalar_subquery )  
    | { unary_operator } expression   
    | expression { binary_operator } expression   
}  
[ COLLATE { Windows_collation_name ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|----------|----------------|  
|*constant*|É um símbolo que representa um valor de dados único e específico. Para obter mais informações, consulte [constantes &#40; Transact-SQL &#41; ](../../t-sql/data-types/constants-transact-sql.md).|  
|*scalar_function*|É uma unidade de [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe que fornece um serviço específico e retorna um único valor. *scalar_function* podem ser funções escalares internas, como as funções SUM, GETDATE ou CAST ou funções escalares definidas pelo usuário.|  
|[ *table_name *.* * ]|É o nome ou alias de uma tabela.|  
|*column*|É o nome de uma coluna. Somente o nome da coluna é permitido em uma expressão.|  
|*variable*|É o nome de uma variável ou parâmetro. Para obter mais informações, consulte [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).|  
|**(** *expression*  **)**|É qualquer expressão válida conforme definido neste tópico. Os parênteses são operadores de agrupamento que verificam se todos os operadores na expressão entre parênteses são avaliados antes de a expressão resultante ser combinada com outra.|  
|**(** *scalar_subquery* **)**|É uma subconsulta que retorna um valor. Por exemplo:<br /><br /> `SELECT MAX(UnitPrice)`<br /><br /> `FROM Products`|  
|{ *unary_operator* }|Os operadores unários podem ser aplicados somente a expressões que avaliam qualquer um dos tipos de dados da categoria de tipo de dados numérico. É um operador que tem somente um operando numérico:<br /><br /> + indica um número positivo.<br /><br /> - indica um número negativo.<br /><br /> ~ indica o operador de complemento.|  
|{ *binary_operator* }|É um operador que define a maneira como duas expressões são combinadas para produzir um único resultado. *binary_operator* pode ser um operador aritmético, o operador de atribuição (=), um operador bit a bit, um operador de comparação, um operador lógico, o operador de concatenação de cadeia de caracteres (+) ou um operador unário. Para obter mais informações sobre operadores, consulte [operadores &#40; Transact-SQL &#41; ](../../t-sql/language-elements/operators-transact-sql.md).|  
|*ranking_windowed_function*|É qualquer função de classificação [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações, consulte [funções de classificação &#40; Transact-SQL &#41; ](../../t-sql/functions/ranking-functions-transact-sql.md).|  
|*aggregate_windowed_function*|É qualquer função de agregação [!INCLUDE[tsql](../../includes/tsql-md.md)] com a cláusula OVER. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).|  
  
## <a name="expression-results"></a>Resultados da expressão  
 Em uma expressão simples composta de uma única constante, variável, função escalar ou nome de coluna: o tipo de dados, agrupamento, precisão, escala e valor da expressão é o tipo de dados, agrupamento, precisão, escala e valor do elemento referenciado.  
  
 Quando duas expressões são combinadas usando operadores lógicos ou de comparação, o tipo de dados resultante é booliano e o valor é um dos seguintes: TRUE, FALSE ou UNKNOWN. Para obter mais informações sobre tipos de dados booleano, consulte [operadores de comparação &#40; Transact-SQL &#41; ](../../t-sql/language-elements/comparison-operators-transact-sql.md).  
  
 Quando duas expressões são combinadas usando operadores aritméticos, bit a bit ou de cadeia de caracteres, o operador determina o tipo de dados resultante.  
  
 Expressões complexas compostas de muitos símbolos e operadores são avaliadas como um único resultado avaliado. O tipo de dados, o agrupamento, a precisão, a escala e o valor da expressão resultante são determinados pela combinação das expressões de componentes, duas de cada vez, até o resultado final ser alcançado. A sequência na qual as expressões são combinadas é definida pela precedência dos operadores na expressão.  
  
## <a name="remarks"></a>Remarks  
 Duas expressões podem ser combinadas por um operador se o operador oferecer suporte para os tipos de dados das duas e pelo menos uma destas condições for verdadeira:  
  
-   As expressões têm o mesmo tipo de dados.  
  
-   O tipo de dados com a menor precedência pode ser implicitamente convertido em tipo de dados com a maior precedência de tipo de dados.  
  
 Se as expressões não atenderem a essas condições, as funções CAST ou CONVERT poderão ser usadas para converter explicitamente o tipo de dados de menor precedência em qualquer tipo de dados de maior precedência ou em um tipo de dados intermediário que possa ser implicitamente convertido no tipo de dados com a maior precedência.  
  
 Se não houver nenhuma conversão implícita ou explícita com suporte, as duas expressões não poderão ser combinadas.  
  
 O agrupamento de qualquer expressão avaliada como uma cadeia de caracteres é definido seguindo as regras de precedência de agrupamento. Para obter mais informações, consulte [precedência de agrupamento &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
 Em uma linguagem de programação como C ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], uma expressão sempre é avaliada como um único resultado. As expressões em uma lista de seleção [!INCLUDE[tsql](../../includes/tsql-md.md)] seguem uma variação nessa regra: a expressão é avaliada individualmente para cada linha no conjunto de resultados. Uma única expressão pode ter um valor diferente em cada linha do conjunto de resultados, mas cada linha tem apenas um valor para a expressão. Por exemplo, na seguinte instrução `SELECT`, as referências a `ProductID` e ao termo `1+2` na lista de seleção são expressões:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, 1+2  
FROM Production.Product;  
GO  
```  
  
 A expressão `1+2` é avaliada como `3` em cada linha do conjunto de resultados. Embora a expressão `ProductID` gere um valor exclusivo em cada linha de conjunto de resultados, cada linha tem apenas um valor para `ProductID`.  
  
## <a name="see-also"></a>Consulte também  
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)   
 [Conversão de tipo de dados &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Precedência de tipo de dados &#40; Transact-SQL &#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [NULLIF &#40;Transact-SQL&#41;](../../t-sql/language-elements/nullif-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
