---
title: STRING_AGG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf74698e9e61f456726b1e6a62126a8d78a09777
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="stringagg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena os valores das expressões de cadeia de caracteres e coloca os valores de separador entre eles. O separador não é adicionado ao final da cadeia de caracteres.
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>Argumentos 

*separador*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de `NVARCHAR` ou `VARCHAR` concatenados de tipo que é usado como separador de cadeias de caracteres. Ele pode ser literal ou variável. 

*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo. Expressões são convertidas em `NVARCHAR` ou `VARCHAR` tipos durante a concatenação. Tipos de cadeia de caracteres não são convertidos em `NVARCHAR` tipo.


< order_clause >   
Opcionalmente, especificar a ordem dos resultados concatenados usando `WITHIN GROUP` cláusula:
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
< order_by_expression_list >   
 
  Uma lista de não constante [expressões](../../t-sql/language-elements/expressions-transact-sql.md) que pode ser usada para classificar os resultados. Apenas um `order_by_expression` é permitida por consulta. A ordem de classificação padrão é crescente.   
  

## <a name="return-types"></a>Tipos de retorno 

Tipo de retorno é depende do primeiro argumento (expressão). Se o argumento de entrada é o tipo de cadeia de caracteres (`NVARCHAR`, `VARCHAR`), tipo de resultado será o mesmo como o tipo de entrada. A tabela a seguir lista as conversões automáticas:  

|Tipo de expressão de entrada |Resultado | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR (1... 4000) |NVARCHAR (4000) |
|VARCHAR (1... 8000) |VARCHAR(8000) |
|int, bigint, smallint, tinyint, numérico, float, real, bit, decimal, smallmoney, money, datetime, datetime2, |NVARCHAR (4000) |


## <a name="remarks"></a>Comentários  
 
`STRING_AGG`agregação usa todas as expressões de linhas e os concatena em uma única cadeia de caracteres. Valores de expressão são implicitamente convertidos em tipos de cadeia de caracteres e depois concatenados. A conversão implícita em cadeias de caracteres segue as regras existentes para conversões de tipo de dados. Para obter mais informações sobre conversões de tipo de dados, consulte [CAST e CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Se a expressão de entrada é o tipo `VARCHAR`, o separador não pode ser um tipo `NVARCHAR`. 

Valores nulos são ignorados e o separador correspondente não será adicionado. Para retornar um espaço reservado para valores nulos, use o `ISNULL` funcione conforme demonstrado no exemplo B.

`STRING_AGG`está disponível em qualquer nível de compatibilidade.


## <a name="examples"></a>Exemplos 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. Gerar a lista de nomes separados em novas linhas 
O exemplo a seguir produz uma lista de nomes em uma célula de resultado único, separados com retornos de carro.
```tsql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`NULL`os valores encontrados em `name` células não são retornadas no resultado.   
> [!NOTE]  
>  Se usar o Editor de consulta do Management Studio, o **resultados em grade** opção não pode implementar o retorno de carro. Alternar para **resultados em texto** ver o resultado definido corretamente.   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. Gerar a lista de nomes separados por vírgula sem valores nulos   
O exemplo a seguir substitui valores nulos com n '/' e retorna os nomes separados por vírgulas em uma célula de resultado.  
```tsql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|CSV | 
|--- |
|John, n/d, Mike, Peter, n/d, n/d, Alice, Bob |  


### <a name="c-generate-comma-separated-values"></a>C. Gerar valores separados por vírgula 

```tsql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|nomes | 
|--- |
|Ken Sánchez (8 de fevereiro de 2003 12:00 AM) <br />Terri Duffy (24 de fevereiro de 2002 12:00 AM) <br />Roberto Tamburello (5 de dez de 2001 12:00 AM) <br />Rob Walters (29 de dez de 2001 12:00 AM) <br />... |

> [!NOTE]  
>  Se usar o Editor de consulta do Management Studio, o **resultados em grade** opção não pode implementar o retorno de carro. Alternar para **resultados em texto** ver o resultado definido corretamente.   
 

### <a name="d-return-news-articles-with-related-tags"></a>D. Retorno de artigos de notícias com marcas relacionadas 

Artigo e suas marcas são separadas em tabelas diferentes. Desenvolvedor quer retornar uma linha por cada artigo com todas as marcas associadas. Usando a seguinte consulta: 
```tsql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |marcas |
|--- |--- |--- |
|172 |Pesquisas indicam os resultados de eleição fechar |política, votações, cidade conselho | 
|176 |Novo estrada esperada para reduzir o congestionamento |NULL |
|177 |Cachorros continuam a ser mais populares que gatos |pesquisas, animais| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. Gerar a lista de endereços de email por cidades

A consulta a seguir localiza os endereços de email dos funcionários e os agrupa por cidades: 
```tsql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Cidade |emails |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

Emails retornado nos emails de coluna pode ser usada para enviar emails ao grupo de pessoas que trabalham em algumas cidades específicas diretamente. 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. Gerar uma lista classificada de emails por cidades   
   
Semelhante ao exemplo anterior, a consulta a seguir localiza os endereços de email de funcionários, agrupa por cidade e classifica os emails em ordem alfabética:   
```tsql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Cidade |emails |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>Consulte também  

[Funções de cadeia de caracteres (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  


