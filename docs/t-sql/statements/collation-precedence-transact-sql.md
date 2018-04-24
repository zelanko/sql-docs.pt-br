---
title: Precedência do agrupamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- coercible-default collation label
- precedence [SQL Server], collations
- collation sensitive
- collations [SQL Server], precedence
- explicit collation label [SQL Server]
- implicit collation label
- no-collation label
- collation insensitive
- operators [Transact-SQL], collations
- collation labels
- collation coercion rules
- rules [SQL Server], collations
ms.assetid: 58c4e64b-5634-4c29-aa22-33193282dd27
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a24e23e58e0ba678cba0617b4b029755326912eb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="collation-precedence-transact-sql"></a>Precedência de agrupamento (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  A precedência de agrupamento, também conhecida como regras de coerção de agrupamento, determina o seguinte:  
  
-   O agrupamento do resultado final de uma expressão que é avaliada como uma cadeia de caracteres.  
  
-   O agrupamento usado pelos operadores que diferenciam agrupamentos e que usam entradas de cadeia de caracteres, mas não retornam uma cadeia de caracteres, como LIKE e IN.  
  
 As regras de precedência de agrupamento se aplicam somente a tipos de dados de cadeia de caracteres: **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext**. Os objetos que têm outros tipos de dados não participam de avaliações de agrupamento.  
  
## <a name="collation-labels"></a>Rótulos de agrupamento  
 A tabela a seguir lista e descreve as quatro categorias nas quais são identificados os agrupamentos de todos os objetos. O nome de cada categoria é chamado de rótulo de agrupamento.  
  
|Rótulo de agrupamento|Tipos de objetos|  
|---------------------|----------------------|  
|Padrão coercível|Qualquer variável de cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)], parâmetro, literal ou a saída de uma função interna de catálogo, ou uma função interna que não obtenha entradas de cadeia de caracteres, mas produza uma saída de cadeia de caracteres.<br /><br /> Se o objeto for declarado em uma função definida pelo usuário, procedimento armazenado ou gatilho, ao objeto será atribuído o agrupamento padrão do banco de dados no qual a função, o procedimento armazenado ou o gatilho for criado. Se o objeto for declarado em um lote, ao objeto será atribuído o agrupamento padrão do banco de dados atual da conexão.|  
|X implícito|Uma referência de coluna. O agrupamento da expressão (X) é obtido do agrupamento definido para a coluna na tabela ou exibição.<br /><br /> Mesmo se foi atribuído explicitamente um agrupamento à coluna usando uma cláusula COLLATE na instrução CREATE TABLE ou CREATE VIEW, a referência da coluna será classificada como implícita.|  
|X explícito|Uma expressão que é convertida explicitamente em um agrupamento específico (X) usando uma cláusula COLLATE na expressão.|  
|Sem-agrupamento|Indica que o valor de uma expressão é o resultado de uma operação entre duas cadeias de caracteres que têm agrupamentos conflitantes do rótulo de agrupamento implícito. O resultado da expressão é definido como não tendo um agrupamento.|  
  
## <a name="collation-rules"></a>Regras de agrupamento  
 O rótulo de agrupamento de uma expressão simples que faça referência a somente um objeto de cadeia de caracteres é o rótulo de agrupamento do objeto referenciado.  
  
 O rótulo de agrupamento de uma expressão complexa que faça referência a duas expressões de operando com o mesmo rótulo de agrupamento é o rótulo de agrupamento das expressões de operando.  
  
 O rótulo de agrupamento do resultado final de uma expressão complexa que faça referência a duas expressões de operando com agrupamentos diferentes tem como base as seguintes regras:  
  
-   Explícito tem precedência sobre implícito. Implícito tem precedência sobre Padrão coercível:  
  
     Explícito >Implícito > Padrão coercível  
  
-   A combinação de duas expressões explícitas que receberam agrupamentos diferentes gera um erro:  
  
     X explícito + Y explícito = Erro  
  
-   A combinação de duas expressões implícitas que tenham agrupamentos diferentes gera um resultado Sem-agrupamento:  
  
     X implícito + Y implícito = Sem-agrupamento  
  
-   A combinação de uma expressão Sem-agrupamento com uma expressão de qualquer rótulo, exceto agrupamento Explícito (consulte a regra seguinte), gera um resultado que tem o rótulo Sem-agrupamento:  
  
     Sem-agrupamento + qualquer coisa = Sem-agrupamento  
  
-   A combinação de uma expressão Sem-agrupamento com uma expressão que tenha um agrupamento Explícito, gera uma expressão com um rótulo Explícito:  
  
     Sem-agrupamento + X explícito = Explícito  
  
 A tabela a seguir resume as regras.  
  
|Rótulo de coerção do operando|X explícito|X implícito|Padrão coercível|Sem-agrupamento|  
|----------------------------|----------------|----------------|------------------------|-------------------|  
|**Y explícito**|Gera erro|O resultado é Y explícito|O resultado é Y explícito|O resultado é Y explícito|  
|**Y implícito**|O resultado é X explícito|O resultado é Sem-agrupamento|O resultado é Y implícito|O resultado é Sem-agrupamento|  
|**Coercible-default**|O resultado é X explícito|O resultado é X implícito|O resultado é Padrão coercível|O resultado é Sem-agrupamento|  
|**Sem agrupamento**|O resultado é X explícito|O resultado é Sem-agrupamento|O resultado é Sem-agrupamento|O resultado é Sem-agrupamento|  
  
 As regras adicionais a seguir também são aplicadas à precedência de agrupamento:  
  
-   Você não pode ter várias cláusulas COLLATE em uma expressão que já é uma expressão explícita. Por exemplo, a seguinte cláusula `WHERE` não é válida porque uma cláusula `COLLATE` foi especificada para uma expressão que já é uma expressão explícita:  
  
     `WHERE ColumnA = ( 'abc' COLLATE French_CI_AS) COLLATE French_CS_AS`  
  
-   Não são permitidas conversões de página de código em tipos de dados **text**. Você não pode converter uma expressão **text** de um agrupamento em outro se eles tiverem páginas de código diferentes. O operador de atribuição não pode atribuir valores quando o agrupamento do operando de texto da direita tiver uma página de código diferente que a do operando de texto da esquerda.  
  
 A precedência de agrupamento é determinada após a conversão de tipo de dados. O operando a partir do qual o agrupamento resultante é obtido pode ser diferente do operando que fornece o tipo de dados do resultado final. Por exemplo, considere o seguinte lote:  
  
```  
CREATE TABLE TestTab  
   (PrimaryKey int PRIMARY KEY,  
    CharCol char(10) COLLATE French_CI_AS  
   )  
  
SELECT *  
FROM TestTab  
WHERE CharCol LIKE N'abc'  
```  
  
 O tipo de dados Unicode da expressão simples `N'abc'` tem uma precedência de tipo de dados mais alta. Portanto, a expressão resultante tem o tipo de dados Unicode atribuído a `N'abc'`. Entretanto, a expressão `CharCol` tem um rótulo de agrupamento Implícito e `N'abc'` tem um rótulo de coerção inferior, Padrão coercível. Assim, o agrupamento usado será `French_CI_AS` de `CharCol`.  
  
### <a name="examples-of-collation-rules"></a>Exemplos de regras de agrupamento  
 Os exemplos a seguir mostram como funcionam as regras de agrupamento. Para executar os exemplos, crie a seguinte tabela de teste.  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE TestTab (  
   id int,   
   GreekCol nvarchar(10) collate greek_ci_as,   
   LatinCol nvarchar(10) collate latin1_general_cs_as  
   )  
INSERT TestTab VALUES (1, N'A', N'a');  
GO  
```  
  
#### <a name="collation-conflict-and-error"></a>Conflito e erro de agrupamento  
 O predicado da consulta a seguir tem conflito de agrupamento e gera um erro.  
  
```  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 448, Level 16, State 9, Line 2  
Cannot resolve collation conflict between 'Latin1_General_CS_AS' and 'Greek_CI_AS' in equal to operation.  
```  
  
#### <a name="explicit-label-vs-implicit-label"></a>Rótulo explícito x rótulo implícito  
 O predicado na consulta a seguir é avaliado no agrupamento `greek_ci_as` porque a expressão da direita tem o rótulo Explícito. Isto tem precedência sobre o rótulo Implícito da expressão da esquerda.  
  
```  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol COLLATE greek_ci_as;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
id          GreekCol             LatinCol  
----------- -------------------- --------------------  
          1 A                    a  
  
(1 row affected)  
```  
  
#### <a name="no-collation-labels"></a>Rótulos sem-agrupamento  
 As expressões `CASE` das consultas a seguir têm um rótulo Sem-agrupamento; portanto, não podem aparecer na lista de seleção ou serem operadas por operadores que diferenciam agrupamentos. Entretanto, as expressões podem ser operadas por operadores que não diferenciem agrupamentos.  
  
```  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END)   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 451, Level 16, State 1, Line 1  
Cannot resolve collation conflict for column 1 in SELECT statement.  
```  
  
```  
SELECT PATINDEX((CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END), 'a')  
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 446, Level 16, State 9, Server LEIH2, Line 1  
Cannot resolve collation conflict for patindex operation.  
```  
  
```  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END) COLLATE Latin1_General_CI_AS   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------  
a  
  
(1 row affected)  
```  
  
## <a name="collation-sensitive-and-collation-insensitive"></a>Diferenciação de agrupamentos e sem diferenciação de agrupamentos  
 Os operadores e as funções diferenciam ou não agrupamentos.  
  
 Diferencia agrupamento  
 Isto significa que a especificação de um operando Sem-agrupamento é um erro em tempo de compilação. O resultado de expressão não pode ser Sem-agrupamento.  
  
 Não diferencia agrupamento  
 Isto significa que os operandos e o resultado podem ser Sem-agrupamento.  
  
### <a name="operators-and-collation"></a>Operadores e agrupamento  
 Os operadores de comparação e os operadores MAX, MIN, BETWEEN, LIKE e IN diferenciam agrupamentos. A cadeia de caracteres usada pelos operadores recebe o rótulo do agrupamento do operando que tem a precedência mais alta. O operador UNION também diferencia agrupamentos e todos os operandos de cadeias de caracteres, além do resultado final, recebem o agrupamento do operando com a precedência mais alta. A precedência de agrupamento dos operandos UNION e do resultado é avaliada a cada coluna.  
  
 O operador de atribuição não diferencia agrupamentos e a expressão da direita é convertida no agrupamento da esquerda.  
  
 O operador de concatenação de cadeias de caracteres não diferencia agrupamentos, e os dois operandos de cadeias de caracteres e o resultado recebem o rótulo de agrupamento do operando com a precedência de agrupamento mais alta. O operador UNION ALL e CASE não diferenciam agrupamentos, e todos os operandos de cadeias de caracteres, além dos resultados finais, recebem o rótulo do agrupamento do operando com a precedência mais alta. A precedência de agrupamento dos operandos UNION ALL e do resultado é avaliada a cada coluna.  
  
### <a name="functions-and-collation"></a>Funções e agrupamento  
 As funções CAST, CONVERT e COLLATE diferenciam agrupamento para os tipos de dados **char**, **varchar** e **text**. Se a entrada e a saída das funções CAST e CONVERT forem cadeias de caracteres, a cadeia de saída terá o rótulo de agrupamento da cadeia de caracteres de entrada. Se a entrada não for uma cadeia de caracteres, a cadeia de saída será Padrão coercível e receberá o agrupamento do banco de dados atual da conexão, ou o banco de dados que contém a função definida pelo usuário, o procedimento armazenado ou o gatilho no qual CAST ou CONVERT é referenciado.  
  
 Para as funções internas que retornam uma cadeia de caracteres, mas não obtêm uma entrada de cadeia, a cadeia resultante será Padrão coercível e receberá o agrupamento do banco de dados atual ou o agrupamento do banco de dados que contém a função definida pelo usuário, o procedimento armazenado ou o gatilho no qual a função é referenciada.  
  
 As funções a seguir diferenciam agrupamentos e suas cadeias de saída têm o rótulo de agrupamento da cadeia de caracteres de entrada:  
  
|||  
|-|-|  
|CHARINDEX|REPLACE|  
|DIFFERENCE|REVERSE|  
|ISNUMERIC|RIGHT|  
|LEFT|SOUNDEX|  
|LEN|STUFF|  
|LOWER|SUBSTRING|  
|PATINDEX|UPPER|  
  
## <a name="see-also"></a>Consulte Também  
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
