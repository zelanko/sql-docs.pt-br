---
title: CHARINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHARINDEX
- CHARINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], pattern searching
- CHARINDEX function
- pattern searching [SQL Server]
- starting point of expression in character string
ms.assetid: 78c10341-8373-4b30-b404-3db20e1a3ac4
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5049508aac52724bbf0b05c9962b154db7af1474
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Pesquisa uma expressão para outra e retorna sua posição inicial, se for localizada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*expressionToFind*  
É um caractere [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que contém a sequência a ser localizada. *expressionToFind* é limitado a 8000 caracteres.
  
*expressionToSearch*  
É uma expressão de caractere a ser pesquisada.
  
*start_location*  
É um **inteiro** ou **bigint** expressão em que a pesquisa inicia. Se *start_location* não for especificado, é um número negativo ou é 0, a pesquisa começará no início do *expressionToSearch*.
  
## <a name="return-types"></a>Tipos de retorno
**bigint** se *expressionToSearch* é o **varchar (max)**, **nvarchar (max)**, ou **varbinary (max)** dados tipos; Caso contrário, **int**.
  
## <a name="remarks"></a>Comentários  
Se qualquer um dos *expressionToFind* ou *expressionToSearch* é de um tipo de dados Unicode (**nvarchar** ou **nchar**) e o outro não, o outra será convertida em um tipo de dados Unicode. CHARINDEX não pode ser usado com **texto**, **ntext**, e **imagem** tipos de dados.
  
Se qualquer um dos *expressionToFind* ou *expressionToSearch* for NULL, CHARINDEX retornará NULL.
  
Se *expressionToFind* não foi encontrado em *expressionToSearch*, CHARINDEX retornará 0.
  
CHARINDEX efetua comparações com base no agrupamento da entrada. Para executar uma comparação em um agrupamento especificado, é possível usar COLLATE para aplicar um agrupamento explícito à entrada.
  
A posição inicial retornada é com base em 1, não com base em 0.
  
0x0000 (**char(0)**) é um caractere indefinido em agrupamentos do Windows e não pode ser incluído em CHARINDEX.
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
Ao usar agrupamentos SC, ambos *start_location* e o valor de retorno contam pares substitutos como um caractere, não dois. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-starting-position-of-an-expression"></a>A. Retornando a posição inicial de uma expressão  
O exemplo a seguir retorna a posição na qual a sequência de caracteres `bicycle` inicia na coluna `DocumentSummary` da tabela `Document` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
DECLARE @document varchar(64);  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bicycle', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
48            
```  
  
### <a name="b-searching-from-a-specific-position"></a>B. Pesquisando em uma posição específica  
O exemplo a seguir usa opcional *start_location* parâmetro para iniciar a procura por `vital` no quinto caractere do `DocumentSummary` coluna o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('vital', @document, 5);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
16            
  
(1 row(s) affected)  
```  
  
### <a name="c-searching-for-a-nonexistent-expression"></a>C. Pesquisando uma expressão inexistente  
A exemplo a seguir mostra o conjunto de resultados quando *expressionToFind* não foi encontrado em *expressionToSearch*.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `0`  
  
`(1 row(s) affected)`
  
### <a name="d-performing-a-case-sensitive-search"></a>D. Executando uma pesquisa com diferenciação de maiúsculas e minúsculas  
O exemplo a seguir executa uma pesquisa diferencia maiusculas de minúsculas para a cadeia de caracteres `'TEST'` em `'This is a Test``'`.
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `0`  
  
O exemplo a seguir executa uma pesquisa diferencia maiusculas de minúsculas para a cadeia de caracteres `'Test'` em `'This is a Test'`.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `13`  
  
### <a name="e-performing-a-case-insensitive-search"></a>E. Executando uma pesquisa sem diferenciação de maiúsculas e minúsculas  
O exemplo a seguir executa uma pesquisa que não diferencia maiúsculas e minúsculas para a cadeia de caracteres `'TEST'` em `'This is a Test'`.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CI_AS);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`-----------`
  
 `13`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. Pesquisar desde o início de uma expressão de cadeia de caracteres  
O exemplo a seguir retorna o primeiro local do `is` de cadeia de caracteres em `This is a string`, a partir da posição 1 (o primeiro caractere) na cadeia de caracteres.
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`---------`
  
 `3`  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. Busca a partir de uma posição que não seja a primeira posição  
O exemplo a seguir retorna o primeiro local do `is` de cadeia de caracteres em `This is a string`, começando com a quarta posição.
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`---------`
  
 `6`  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. Ocorre quando a cadeia de caracteres não foi encontrada.  
A exemplo a seguir mostra o valor de retorno quando o *string_pattern* não foi encontrado na cadeia de caracteres pesquisada.
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`---------`
  
 `0`  
  
## <a name="see-also"></a>Consulte também
[Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[+ &#40; Concatenação de cadeia de caracteres &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
[Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
  
  



