---
title: Critério de pesquisa (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- search
- Search Condition
- condition
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator [Transact-SQL]
- CONTAINS predicate (Transact-SQL)
- ESCAPE keyword
- operators [Transact-SQL], search condition
- search conditions [SQL Server]
- WHERE clause, search conditions
- ALL keyword
- FREETEXT predicate (Transact-SQL)
- EXISTS keyword
- search conditions [SQL Server], about search conditions
- NOT operator [Transact-SQL]
- BETWEEN operator
- SOME | ANY keyword
- predicates [full-text search]
- AND, about search conditions
- logical operators [SQL Server], about search conditions
- precedence [SQL Server], logical operators
- logical operators [SQL Server], precedence
- LIKE comparisons
ms.assetid: 09974469-c5d2-4be8-bc5a-78e404660b2c
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6ffe7a15fdaa81492cf0b993ba10a1ca555c6625
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38066634"
---
# <a name="search-condition-transact-sql"></a>Critério de pesquisa (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  É uma combinação de um ou mais predicados que usam os operadores lógicos AND, OR e NOT.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<search_condition> ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '<contains_search_condition>' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery )     }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
< search_condition > ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | < | < = } expression   
    | string_expression [ NOT ] LIKE string_expression   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | expression [ NOT ] IN (subquery | expression [ ,...n ] )   
    | expression [ NOT ] EXISTS (subquery)     }   
```  
  
## <a name="arguments"></a>Argumentos  
 \<search_condition>  
 Especifica as condições para as linhas retornadas no conjunto de resultados para uma instrução SELECT, expressão de consulta ou subconsulta. Para uma instrução UPDATE, especifica as linhas a serem atualizadas. Para uma instrução DELETE, especifica as linhas a serem excluídas. Não há nenhum limite para o número de predicados que podem ser incluídos em um critério de pesquisa da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 NOT  
 Nega a expressão booliana especificada pelo predicado. Para obter mais informações, consulte [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md).  
  
 AND  
 Combina duas condições e avalia como TRUE quando ambas são TRUE. Para obter mais informações, consulte [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md).  
  
 OU  
 Combina duas condições e avalia como TRUE quando uma delas é TRUE. Para obter mais informações, consulte [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md).  
  
 \< predicate >  
 É uma expressão que retorna TRUE, FALSE ou UNKNOWN.  
  
 *expressão*  
 É um nome de coluna, uma constante, uma função, uma variável, uma subconsulta escalar ou qualquer combinação de nomes de colunas, constantes e funções conectadas por um operador ou operadores ou por uma subconsulta. A expressão também pode conter a expressão CASE.  
  
> [!NOTE]  
>  Variáveis e constantes de cadeia de caracteres não Unicode usam a página de código que corresponde ao agrupamento padrão do banco de dados. As conversões de página de código podem ocorrer ao trabalhar somente com os dados de caractere não Unicode e referenciar os tipos de dados de caractere não Unicode **char**, **varchar** e **text**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte variáveis e constantes de cadeia de caracteres não Unicode na página de código que corresponde ao agrupamento da coluna referenciada ou especificada com COLLATE, caso a página de código seja diferente da página de código que corresponde ao agrupamento padrão do banco de dados. Os caracteres não encontrados na nova página de código serão convertidos em um caractere semelhante se um [mapeamento de melhor ajuste](http://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/) puder ser encontrado; caso contrário, eles serão convertidos no caractere de substituição padrão "?".  
>  
> Ao trabalhar com várias páginas de código, as constantes de caractere podem ser prefixadas com a letra maiúscula 'N', e as variáveis Unicode podem ser usadas, a fim de evitar conversões de página de código.  
  
 =  
 É o operador usado para testar a igualdade entre duas expressões.  
  
 <>  
 É o operador usado para testar a condição de duas expressões que não são iguais.  
  
 !=  
 É o operador usado para testar a condição de duas expressões que não são iguais.  
  
 \>  
 É o operador usado para testar a condição de uma expressão maior do que a outra.  
  
 \>=  
 É o operador usado para testar a condição de uma expressão maior que ou igual a outra.  
  
 !>  
 É o operador usado para testar a condição de uma expressão que não é maior que a outra.  
  
 <  
 É o operador usado para testar a condição de uma expressão menor do que a outra.  
  
 <=  
 É o operador usado para testar a condição de uma expressão menor que ou igual a outra.  
  
 !<  
 É o operador usado para testar a condição de uma expressão que não é menor que a outra.  
  
 *string_expression*  
 É uma cadeia de caracteres e caracteres e curinga.  
  
 [ NOT ] LIKE  
 Indica que a cadeia de caracteres subsequente será usada com uma correspondência de padrão. Para obter mais informações, consulte [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md).  
  
 ESCAPE **'***escape_ character***'**  
 Permite pesquisar um caractere curinga em uma cadeia de caracteres, em vez de funcionar como um curinga. *escape_character* é o caractere colocado na frente do caractere curinga para indicar esse uso especial.  
  
 [ NOT ] BETWEEN  
 Especifica um intervalo inclusivo de valores. Use AND para separar os valores inicial e final. Para obter mais informações, consulte [BETWEEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/between-transact-sql.md).  
  
 IS [ NOT ] NULL  
 Especifica uma pesquisa de valores nulos ou de valores não nulos, dependendo das palavras-chave usadas. Uma expressão com um operador bit a bit ou aritmético avaliará como NULL se qualquer um dos operandos for NULL.  
  
 CONTAINS  
 Pesquisa colunas que contêm tipos de dados baseados em caracteres para obter correspondências precisas ou menos precisas (*difusas*) para palavras e frases únicas, proximidade entre palavras dentro de determinada distância e correspondências ponderadas. Esta opção só pode ser usada com instruções SELECT. Para obter mais informações, consulte [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md).  
  
 FREETEXT  
 Fornece uma forma simples de consulta de idioma natural pesquisando colunas que contêm dados baseados em caracteres para obter valores que correspondam ao significado em vez das palavras exatas no predicado. Esta opção só pode ser usada com instruções SELECT. Para obter mais informações, consulte [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md).  
  
 [ NOT ] IN  
 Especifica a pesquisa de uma expressão, com base na inclusão ou exclusão da expressão em uma lista. A expressão da pesquisa pode ser uma constante ou um nome de coluna, e a lista pode ser um conjunto de constantes ou, normalmente, uma subconsulta. Inclua a lista de valores em parênteses. Para obter mais informações, consulte [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md).  
  
 *subquery*  
 Pode ser considerada uma instrução SELECT restrita e é semelhante a \<query_expresssion> na instrução SELECT. A cláusula ORDER BY e a palavra-chave INTO não são permitidas. Para obter mais informações, consulte [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
 ALL  
 Usado com um operador de comparação e uma subconsulta. Retorna TRUE para \<predicate> quando todos os valores recuperados para a subconsulta atendem à operação de comparação ou FALSE quando nem todos os valores atendem à comparação ou quando a subconsulta não retorna nenhuma linha para a instrução externa. Para obter mais informações, consulte [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md).  
  
 { SOME | ANY }  
 Usado com um operador de comparação e uma subconsulta. Retorna TRUE para \<predicate> quando qualquer valor recuperado para a subconsulta atende à operação de comparação ou FALSE quando nenhum valor na subconsulta atende à comparação, ou quando a subconsulta não retorna nenhuma linha para a instrução externa. Caso contrário, a expressão é UNKNOWN. Para obter mais informações, consulte [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 EXISTS  
 Usada com uma subconsulta para testar para a existência de linhas retornadas pela subconsulta. Para obter mais informações, consulte [EXISTS &#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 A ordem de precedência para operadores lógicos é NOT (mais alto), seguido por AND, seguido por OR. Podem ser usados parênteses para substituir essa precedência em uma condição de pesquisa. A ordem de avaliação de operadores lógicos pode variar, dependendo das escolhas feitas pelo otimizador de consultas. Para obter mais informações sobre como os operadores lógicos funcionam em valores lógicos, consulte [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md), [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md) e [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-where-with-like-and-escape-syntax"></a>A. Usando a sintaxe WHERE com LIKE e ESCAPE  
 O exemplo a seguir pesquisa as linhas nas quais a coluna `LargePhotoFileName` tem os caracteres `green_` e usa a opção `ESCAPE` porque _ é um caractere curinga. Sem especificar a opção `ESCAPE`, a consulta pesquisará quaisquer valores de descrição que contêm a palavra `green` seguida de qualquer caractere único diferente do caractere _.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT *   
FROM Production.ProductPhoto  
WHERE LargePhotoFileName LIKE '%greena_%' ESCAPE 'a' ;  
```  
  
### <a name="b-using-where-and-like-syntax-with-unicode-data"></a>B. Usando a sintaxe WHERE e LIKE com dados Unicode  
 O exemplo a seguir usa a cláusula `WHERE` para recuperar o endereço para correspondência para qualquer empresa que esteja fora dos Estados Unidos  (`US`) e em uma cidade cujo nome comece com `Pa`.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT AddressLine1, AddressLine2, City, PostalCode, CountryRegionCode    
FROM Person.Address AS a  
JOIN Person.StateProvince AS s ON a.StateProvinceID = s.StateProvinceID  
WHERE CountryRegionCode NOT IN ('US')  
AND City LIKE N'Pa%' ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-where-with-like"></a>C. Usando WHERE com LIKE  
 O exemplo a seguir pesquisa as linhas nas quais a coluna `LastName` tem os caracteres `and`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE '%and%';  
```  
  
### <a name="d-using-where-and-like-syntax-with-unicode-data"></a>D. Usando a sintaxe WHERE e LIKE com dados Unicode  
 O exemplo a seguir usa a cláusula `WHERE` para realizar uma pesquisa Unicode na coluna `LastName`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE N'%and%';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

