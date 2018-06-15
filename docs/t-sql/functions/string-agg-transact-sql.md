---
title: STRING_AGG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 7c270729aa66c05f835cba507884e8d5cda102d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33063553"
---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena os valores das expressões de cadeia de caracteres e coloca os valores de separador entre eles. O separador não é adicionado ao final da cadeia de caracteres.
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>Argumentos 

*separator*  
É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) do tipo `NVARCHAR` ou `VARCHAR` que é usada como separador de cadeias de caracteres concatenadas. Pode ser um literal ou uma variável. 

*expressão*  
É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo. As expressões são convertidas em tipos `NVARCHAR` ou `VARCHAR` durante a concatenação. Tipos que não são uma cadeia de caracteres são convertidos no tipo `NVARCHAR`.


<order_clause>   
Opcionalmente, especifique a ordem dos resultados concatenados usando a cláusula `WITHIN GROUP`:
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
<order_by_expression_list>   
 
  Uma lista de [expressions](../../t-sql/language-elements/expressions-transact-sql.md) de não constante que pode ser usada para classificar os resultados. Apenas uma `order_by_expression` é permitida por consulta. A ordem de classificação padrão é crescente.   
  

## <a name="return-types"></a>Tipos de retorno 

O tipo de retorno depende do primeiro argumento (expressão). Se o argumento de entrada for um tipo de cadeia de caracteres (`NVARCHAR`, `VARCHAR`), o tipo de resultado será o mesmo do tipo de entrada. A seguinte tabela lista as conversões automáticas:  

|Tipo de expressão de entrada |Resultado | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR(1…4000) |NVARCHAR(4000) |
|VARCHAR(1…8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, numeric, float, real, bit, decimal, smallmoney, money, datetime e datetime2 |NVARCHAR(4000) |


## <a name="remarks"></a>Remarks  
 
`STRING_AGG` é uma função de agregação que usa todas as expressões de linhas e concatena-as em uma única cadeia de caracteres. Os valores de expressão são convertidos implicitamente em tipos de cadeia de caracteres e depois concatenados. A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Para obter mais informações sobre conversões de tipo de dados, consulte [CAST e CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Se a expressão de entrada for um tipo `VARCHAR`, o separador não poderá ser um tipo `NVARCHAR`. 

Valores nulos são ignorados e o separador correspondente não é adicionado. Para retornar um espaço reservado para valores nulos, use a função `ISNULL`, conforme demonstrado no exemplo B.

`STRING_AGG` está disponível em qualquer nível de compatibilidade.


## <a name="examples"></a>Exemplos 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. Gerar a lista de nomes separados em novas linhas 
O exemplo a seguir gera uma lista de nomes em uma única célula de resultados, separados com retornos de carro.
```sql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Davi <br />Catherine <br />Kim <br />Kim <br />Kim <br />Humberto <br />... | 

Os valores de `NULL` encontrados nas células `name` não são retornados no resultado.   
> [!NOTE]  
>  Se você estiver usando o Editor de Consultas do Management Studio, a opção **Resultados em Grade** não poderá implementar o retorno de carro. Alterne para **Resultados em Texto** para ver o conjunto de resultados corretamente.   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. Gerar uma lista de nomes separados por vírgula sem valores NULL   
O exemplo a seguir substitui valores nulos por 'N/A' e retorna os nomes separados por vírgulas em uma única célula de resultados.  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|Csv | 
|--- |
|Julio, N/A, Marco, Pedro, N/A, N/A, Alice, Diogo |  


### <a name="c-generate-comma-separated-values"></a>C. Gerar valores separados por vírgula 

```sql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|nomes | 
|--- |
|Ken Sánchez (Feb 8 2003 12:00AM) <br />Manuela Ribeiro (24 de fev de 2002 24h) <br />Henrique Cunha (5 de dez de 2001 24h) <br />Fábio Pena (29 de dez de 2001 24h) <br />... |

> [!NOTE]  
>  Se você estiver usando o Editor de Consultas do Management Studio, a opção **Resultados em Grade** não poderá implementar o retorno de carro. Alterne para **Resultados em Texto** para ver o conjunto de resultados corretamente.   
 

### <a name="d-return-news-articles-with-related-tags"></a>D. Retornar artigos de notícias com marcas relacionadas 

O artigo e suas marcas são separados em tabelas diferentes. O desenvolvedor deseja retornar uma linha por artigo com todas as marcas associadas. Usando a seguinte consulta: 
```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |marcas |
|--- |--- |--- |
|172 |Pesquisas indicam resultados aproximados da eleição |política, pesquisas, câmara municipal | 
|176 |Previsão de construção de nova estrada para reduzir o congestionamento |NULL |
|177 |Cachorros continuam sendo mais populares do que gatos |pesquisas, animais| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. Gerar uma lista de emails por cidades

A seguinte consulta localiza os endereços de email de funcionários e agrupa-os por cidades: 
```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|cidade |emails |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

Os emails retornados na coluna de emails podem ser usados diretamente para enviar emails ao grupo de pessoas que trabalham em algumas cidades específicas. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. Gerar uma lista classificada de emails por cidades   
   
Semelhante ao exemplo anterior, a seguinte consulta localiza os endereços de email de funcionários, agrupa-os por cidade e classifica os emails em ordem alfabética:   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|cidade |emails |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>Consulte Também  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

