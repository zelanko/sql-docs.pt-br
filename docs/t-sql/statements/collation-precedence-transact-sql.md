---
description: Precedência de ordenação
title: Precedência da ordenação | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 13a960ed74fe9947d82e6dee3701ce1ba6af7648
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124157"
---
# <a name="collation-precedence"></a>Precedência de ordenação
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A precedência de ordenação, também conhecida como regras de coerção de ordenação, determina o seguinte:  
  
-   A ordenação do resultado final de uma expressão que é avaliada como uma cadeia de caracteres.  
  
-   A ordenação usada pelos operadores que diferenciam ordenações e que usam entradas de cadeia de caracteres, mas não retornam uma cadeia de caracteres, como LIKE e IN.  
  
As regras de precedência de ordenação se aplicam somente a tipos de dados de cadeia de caracteres: **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext**. Os objetos que têm outros tipos de dados não participam de avaliações de ordenação.  
  
## <a name="collation-labels"></a>Rótulos de ordenação  
A tabela a seguir lista e descreve as quatro categorias nas quais são identificadas as ordenações de todos os objetos. O nome de cada categoria é chamado de rótulo de ordenação.  
  
|Rótulo de ordenação|Tipos de objetos|  
|---------------------|----------------------|  
|Padrão coercível|Qualquer variável de cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)], parâmetro, literal ou a saída de uma função interna de catálogo, ou uma função interna que não obtenha entradas de cadeia de caracteres, mas produza uma saída de cadeia de caracteres.<br /><br /> Se o objeto for declarado em uma função definida pelo usuário, procedimento armazenado ou gatilho, ao objeto será atribuída a ordenação padrão do banco de dados no qual a função, o procedimento armazenado ou o gatilho for criado. Se o objeto for declarado em um lote, ao objeto será atribuída a ordenação padrão do banco de dados atual da conexão.|  
|X implícito|Uma referência de coluna. A ordenação da expressão (X) é obtida da ordenação definida para a coluna na tabela ou exibição.<br /><br /> Mesmo se foi atribuído explicitamente uma ordenação à coluna usando uma cláusula COLLATE na instrução CREATE TABLE ou CREATE VIEW, a referência da coluna será classificada como implícita.|  
|X explícito|Uma expressão que é convertida explicitamente em uma ordenação específica (X) usando uma cláusula COLLATE na expressão.|  
|Sem-agrupamento|Indica que o valor de uma expressão é o resultado de uma operação entre duas cadeias de caracteres que têm ordenações conflitantes do rótulo de ordenação implícito. O resultado da expressão é definido como não tendo uma ordenação.|  
  
## <a name="collation-rules"></a>Regras de ordenação  
O rótulo de ordenação de uma expressão simples que faça referência a somente um objeto de cadeia de caracteres é o rótulo de ordenação do objeto referenciado.  
  
O rótulo de ordenação de uma expressão complexa que faça referência a duas expressões de operando com o mesmo rótulo de ordenação é o rótulo de ordenação das expressões de operando.  
  
O rótulo de ordenação do resultado final de uma expressão complexa que faça referência a duas expressões de operando com ordenações diferentes tem como base as seguintes regras:  
  
-   Explícito tem precedência sobre implícito. Implícito tem precedência sobre Padrão coercível:  
  
     Explícito > Implícito > Padrão coercível  
  
-   A combinação de duas expressões explícitas que receberam ordenações diferentes gera um erro:  
  
     X explícito + Y explícito = Erro  
  
-   A combinação de duas expressões implícitas que tenham ordenações diferentes gera um resultado Sem-ordenação:  
  
     X implícito + Y implícito = Sem-agrupamento  
  
-   A combinação de uma expressão Sem-ordenação com uma expressão de qualquer rótulo, exceto ordenação Explícita (consulte a regra seguinte), gera um resultado que tem o rótulo Sem-ordenação:  
  
     Sem-agrupamento + qualquer coisa = Sem-agrupamento  
  
-   A combinação de uma expressão Sem-ordenação com uma expressão que tenha uma ordenação Explícita, gera uma expressão com um rótulo Explícito:  
  
     Sem-agrupamento + X explícito = Explícito  
  
A tabela a seguir resume as regras.  
  
|Rótulo de coerção do operando|X explícito|X implícito|Padrão coercível|Sem-agrupamento|  
|----------------------------|----------------|----------------|------------------------|-------------------|  
|**Y explícito**|Gera erro|O resultado é Y explícito|O resultado é Y explícito|O resultado é Y explícito|  
|**Y implícito**|O resultado é X explícito|O resultado é Sem-agrupamento|O resultado é Y implícito|O resultado é Sem-agrupamento|  
|**Coercible-default**|O resultado é X explícito|O resultado é X implícito|O resultado é Padrão coercível|O resultado é Sem-agrupamento|  
|**Sem agrupamento**|O resultado é X explícito|O resultado é Sem-agrupamento|O resultado é Sem-agrupamento|O resultado é Sem-agrupamento|  
  
As regras adicionais a seguir também são aplicadas à precedência de ordenação:  
  
-   Você não pode ter várias cláusulas COLLATE em uma expressão que já é uma expressão explícita. Por exemplo, a seguinte cláusula `WHERE` não é válida porque uma cláusula `COLLATE` foi especificada para uma expressão que já é uma expressão explícita:  
  
     `WHERE ColumnA = ( 'abc' COLLATE French_CI_AS) COLLATE French_CS_AS`  
  
-   Não são permitidas conversões de página de código em tipos de dados **text**. Você não pode converter uma expressão **text** de uma ordenação em outra se elas tiverem páginas de código diferentes. O operador de atribuição não pode atribuir valores quando a ordenação do operando de texto da direita tiver uma página de código diferente que a do operando de texto da esquerda.  
  
A precedência de ordenação é determinada após a conversão de tipo de dados. O operando a partir do qual a ordenação resultante é obtida pode ser diferente do operando que fornece o tipo de dados do resultado final. Por exemplo, considere o seguinte lote:  
  
```sql  
CREATE TABLE TestTab  
   (PrimaryKey int PRIMARY KEY,  
    CharCol char(10) COLLATE French_CI_AS  
   )  
  
SELECT *  
FROM TestTab  
WHERE CharCol LIKE N'abc'  
```  
  
O tipo de dados Unicode da expressão simples `N'abc'` tem uma precedência de tipo de dados mais alta. Portanto, a expressão resultante tem o tipo de dados Unicode atribuído a `N'abc'`. Entretanto, a expressão `CharCol` tem um rótulo de ordenação Implícito e `N'abc'` tem um rótulo de coerção inferior, Padrão coercível. Assim, a ordenação usada será `French_CI_AS` de `CharCol`.  
  
### <a name="examples-of-collation-rules"></a>Exemplos de regras de ordenação  
 Os exemplos a seguir mostram como funcionam as regras de ordenação. Para executar os exemplos, crie a seguinte tabela de teste.  
  
```sql  
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
  
#### <a name="collation-conflict-and-error"></a>Conflito e erro de ordenação  
 O predicado da consulta a seguir tem conflito de ordenação e gera um erro.  
  
```sql  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 448, Level 16, State 9, Line 2  
Cannot resolve collation conflict between 'Latin1_General_CS_AS' and 'Greek_CI_AS' in equal to operation.  
```  
  
#### <a name="explicit-label-vs-implicit-label"></a>Rótulo explícito versus rótulo implícito  
 O predicado na consulta a seguir é avaliado na ordenação `greek_ci_as` porque a expressão da direita tem o rótulo Explícito. Isto tem precedência sobre o rótulo Implícito da expressão da esquerda.  
  
```sql  
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
As expressões `CASE` das consultas a seguir têm um rótulo Sem-ordenação; portanto, não podem aparecer na lista de seleção ou serem operadas por operadores que diferenciam ordenações. Entretanto, as expressões podem ser operadas por operadores que não diferenciem ordenações.  
  
```sql  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END)   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 451, Level 16, State 1, Line 1  
Cannot resolve collation conflict for column 1 in SELECT statement.  
```  
  
```sql  
SELECT PATINDEX((CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END), 'a')  
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 446, Level 16, State 9, Server LEIH2, Line 1  
Cannot resolve collation conflict for patindex operation.  
```  
  
```sql  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END) COLLATE Latin1_General_CI_AS   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------  
a  
  
(1 row affected)  
```  
  
## <a name="collation-sensitive-and-collation-insensitive"></a>Diferenciação de ordenações e sem diferenciação de ordenações  
Os operadores e as funções diferenciam ou não ordenações.  
  
Diferencia ordenação  
Isto significa que a especificação de um operando Sem-agrupamento é um erro em tempo de compilação. O resultado de expressão não pode ser Sem-agrupamento.  
  
Não diferencia ordenação  
Isto significa que os operandos e o resultado podem ser Sem-agrupamento.  
  
### <a name="operators-and-collation"></a>Operadores e ordenação  
Os operadores de comparação e os operadores MAX, MIN, BETWEEN, LIKE e IN diferenciam ordenações. A cadeia de caracteres usada pelos operadores recebe o rótulo da ordenação do operando que tem a precedência mais alta. A instrução UNION também diferencia ordenações e todos os operandos de cadeias de caracteres. Além disso, a ordenação do operando com a precedência mais alta é atribuída ao resultado final. A precedência de ordenação dos operandos UNION e do resultado é avaliada a cada coluna.  
  
O operador de atribuição não diferencia ordenações e a expressão da direita é convertida na ordenação da esquerda.  
  
O operador de concatenação de cadeias de caracteres não diferencia ordenações, e os dois operandos de cadeias de caracteres e o resultado recebem o rótulo de ordenação do operando com a precedência de ordenação mais alta. As instruções UNION ALL e CASE não diferenciam ordenações. Além disso, o rótulo da ordenação do operando com a precedência mais alta é atribuído a todos os operandos de cadeias de caracteres e aos resultados finais. A precedência de ordenação dos operandos UNION ALL e do resultado é avaliada a cada coluna.  
  
### <a name="functions-and-collation"></a>Funções e ordenação  
As funções CAST, CONVERT e COLLATE diferenciam ordenação para os tipos de dados **char**, **varchar** e **text**. Se a entrada e a saída das funções CAST e CONVERT forem cadeias de caracteres, a cadeia de saída terá o rótulo de ordenação da cadeia de caracteres de entrada. Se a entrada não for uma cadeia de caracteres, a cadeia de saída será Padrão coercível e receberá a ordenação do banco de dados atual da conexão, ou o banco de dados que contém a função definida pelo usuário, o procedimento armazenado ou o gatilho no qual CAST ou CONVERT é referenciado.  
  
 Para as funções internas que retornam uma cadeia de caracteres, mas não obtêm uma entrada de cadeia, a cadeia resultante será Padrão coercível e receberá a ordenação do banco de dados atual ou a ordenação do banco de dados que contém a função definida pelo usuário, o procedimento armazenado ou o gatilho no qual a função é referenciada.  
  
 As funções a seguir diferenciam ordenações e suas cadeias de saída têm o rótulo de ordenação da cadeia de caracteres de entrada:  

:::row:::
    :::column:::
        CHARINDEX
    :::column-end:::
    :::column:::
        REPLACE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        DIFFERENCE
    :::column-end:::
    :::column:::
        REVERSE
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        ISNUMERIC
    :::column-end:::
    :::column:::
        RIGHT
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        LEFT
    :::column-end:::
    :::column:::
        SOUNDEX
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        LEN
    :::column-end:::
    :::column:::
        STUFF
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        LOWER
    :::column-end:::
    :::column:::
        SUBSTRING
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        PATINDEX
    :::column-end:::
    :::column:::
        UPPER
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>Consulte Também  
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
