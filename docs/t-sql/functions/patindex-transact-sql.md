---
title: PATINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 51b18437976a9ecb192a69602ecbdc97054b9b47
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76831831"
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna a posição inicial da primeira ocorrência de um padrão em uma expressão específica ou zeros, se o padrão não for encontrado, em todos os tipos de dados de caractere e de texto válidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *pattern*  
 É uma expressão de caractere que contém a sequência a ser localizada. Caracteres curinga podem ser usados; entretanto, o caractere % deve vir antes e seguir *pattern* (exceto quando você pesquisa o primeiro e último caracteres). *pattern* é uma expressão da categoria de tipo de dados de cadeia de caracteres. *pattern* é limitado a 8.000 caracteres.

 > [!NOTE]
 > Embora as expressões regulares tradicionais não sejam nativamente compatíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a correspondência de padrões complexos semelhantes pode ser obtida com o uso de várias expressões curinga. Confira a documentação de [Operações de cadeia de caracteres](../../t-sql/language-elements/string-operators-transact-sql.md) para obter mais detalhes sobre a sintaxe do curinga.
  
 *expressão*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md), geralmente, uma coluna na qual procurar o padrão especificado. *expression* é uma expressão da categoria de tipo de dados de cadeia de caracteres.  
  
## <a name="return-types"></a>Tipos de retorno  
**bigint** se *expression* é dos tipos de dados **varchar(max)** ou **nvarchar(max)** ; caso contrário, **int**.  
  
## <a name="remarks"></a>Comentários  
Se *pattern* ou *expression* for NULL, PATINDEX retornará NULL.  
 
A posição inicial para PATINDEX é 1.
 
PATINDEX executa comparações com base na ordenação da entrada. Para fazer uma comparação em uma ordenação especificada, use COLLATE para aplicar uma ordenação explícita à entrada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
Ao usar ordenações SC, o valor retornado contará os pares alternativos UTF-16 no parâmetro *expression* como um caractere único. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
0x0000 (**char(0)** ) é um caractere indefinido em ordenações do Windows e não pode ser incluído em PATINDEX.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-patindex-example"></a>a. Exemplo simples de PATINDEX  
 O exemplo a seguir verifica uma cadeia de caracteres curta (`interesting data`) em busca do local inicial dos caracteres `ter`.  
  
```sql  
SELECT position = PATINDEX('%ter%', 'interesting data');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
position
--------
3
```
  
### <a name="b-using-a-pattern-with-patindex"></a>B. Usando um padrão com PATINDEX  
O exemplo a seguir localiza a posição na qual o padrão `ensure` inicia em uma linha específica da coluna `DocumentSummary` na tabela `Document` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT position = PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
position
--------  
64  
```  
  
Se você não restringir as linhas a serem pesquisadas usando uma cláusula `WHERE`, a consulta retornará todas as linhas na tabela e registrará valores diferentes de zero para as linhas nas quais o padrão foi localizado e zero para todas as linhas nas quais o padrão não foi localizado.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. Usando caracteres curinga com PATINDEX  
 O exemplo a seguir usa os curingas % e _ para localizar a posição na qual o padrão `'en'`, seguido de qualquer outro caractere e `'ure'` é iniciado na cadeia de caracteres especificada (o índice inicia em 1):  
  
```sql  
SELECT position = PATINDEX('%en_ure%', 'Please ensure the door is locked!');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
position
--------  
8  
```  
  
`PATINDEX` funciona da mesma forma que `LIKE`, então você pode usar qualquer curinga. Não é necessário colocar o padrão entre porcentagens. `PATINDEX('a%', 'abc')` retorna 1 e `PATINDEX('%a', 'cba')` retorna 3.  
  
 Diferentemente de `LIKE`, `PATINDEX` retorna uma posição, semelhante ao que `CHARINDEX` faz.  

### <a name="d-using-complex-wildcard-expressions-with-patindex"></a>D. Usando expressões curinga complexas com PATINDEX 
O exemplo a seguir usa o [operador de cadeia de caracteres](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md) `[^]` para localizar a posição de um caractere que não é um número, uma letra ou um espaço.

```sql
SELECT position = PATINDEX('%[^ 0-9A-z]%', 'Please ensure the door is locked!'); 
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
position
--------
33
```

### <a name="e-using-collate-with-patindex"></a>E. Usando COLLATE com PATINDEX  
 O exemplo a seguir usa a função `COLLATE` para especificar explicitamente a ordenação da expressão que é pesquisada.  
  
```sql  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
position
--------
9
```

### <a name="f-using-a-variable-to-specify-the-pattern"></a>F. Usando uma variável para especificar o padrão  
O exemplo a seguir usa uma variável para passar um valor para o parâmetro *pattern*. Este exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT position = PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
position
--------  
22
```  
  
## <a name="see-also"></a>Consulte Também  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;Curinga – caracteres para correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;Curinga – caracteres para não correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;Curinga – encontrar a correspondência de um caractere&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [Caractere de percentual &#40;Curinga – caracteres para correspondência&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  


