---
title: PATINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abf357840512c1447f0977a151ca742b148f45d2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a posição inicial da primeira ocorrência de um padrão em uma expressão específica ou zeros, se o padrão não for encontrado, em todos os tipos de dados de caractere e de texto válidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *padrão*  
 É uma expressão de caractere que contém a sequência a ser localizada. Caracteres curinga podem ser usados; No entanto, o caractere % deve vir antes e seguir *padrão* (exceto quando você procura primeiro e último caracteres). *padrão de* é uma expressão da categoria de tipo de dados de cadeia de caracteres. *padrão de* é limitado a 8000 caracteres.  
  
 *expressão*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md), normalmente uma coluna que é pesquisada para o padrão especificado. *expressão* é a categoria de tipo de dados de cadeia de caracteres.  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint** se *expressão* é o **varchar (max)** ou **nvarchar (max)** tipos de dados; caso contrário, **int**.  
  
## <a name="remarks"></a>Comentários  
 Se qualquer um dos *padrão* ou *expressão* for NULL, PATINDEX retornará NULL.  
  
 PATINDEX executa comparações com base no agrupamento da entrada. Para executar uma comparação em um agrupamento especificado, é possível usar COLLATE para aplicar um agrupamento explícito à entrada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 Ao usar agrupamentos SC, o valor de retorno contará qualquer par de substituto UTF-16 *expressão* parâmetro como um único caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 0x0000 (**char(0)**) é um caractere indefinido em agrupamentos do Windows e não pode ser incluído em PATINDEX.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-patindex-example"></a>A. Exemplo simples de PATINDEX  
 O exemplo a seguir verifica uma cadeia de caracteres curtas (`interesting data`) para o local inicial dos caracteres `ter`.  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. Usando um padrão com PATINDEX  
 O exemplo a seguir localiza a posição na qual o padrão `ensure` inicia em uma linha específica da coluna `DocumentSummary` na tabela `Document` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
 Se você não restringir as linhas a serem pesquisadas usando uma cláusula `WHERE`, a consulta retornará todas as linhas na tabela e registrará valores diferentes de zero para as linhas nas quais o padrão foi localizado e zero para todas as linhas nas quais o padrão não foi localizado.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. Usando caracteres curinga com PATINDEX  
 O exemplo a seguir usa os curingas % e _ para localizar a posição na qual o padrão `'en'`, seguido de qualquer outro caractere e `'ure'` é iniciado na cadeia de caracteres especificada (o índice inicia em 1):  
  
```  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
 `PATINDEX` funciona da mesma forma que `LIKE`, então você pode usar qualquer curinga. Não é necessário colocar o padrão entre porcentagens. `PATINDEX('a%', 'abc')` retorna 1 e `PATINDEX('%a', 'cba')` retorna 3.  
  
 Diferentemente de `LIKE`, `PATINDEX` retorna uma posição, semelhante ao que `CHARINDEX` faz.  
  
### <a name="d-using-collate-with-patindex"></a>D. Usando COLLATE com PATINDEX  
 O exemplo a seguir usa a função `COLLATE` para especificar explicitamente o agrupamento da expressão que é pesquisada.  
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. Usando uma variável para especificar o padrão  
 O exemplo a seguir usa uma variável para passar um valor para o *padrão* parâmetro. Este exemplo usa o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.  
  
```  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------  
 22
 ```  
  

  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40; Curinga – caracteres &#40; s &#41; a correspondência &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40; Curinga – caracteres &#40; s &#41; Para não coincidir &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40; Curinga – corresponde a um caractere &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [Caractere de porcentagem &#40; Curinga – caracteres &#40; s &#41; a correspondência &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  



