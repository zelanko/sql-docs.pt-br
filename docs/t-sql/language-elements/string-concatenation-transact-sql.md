---
title: "+ (Concatenação de cadeia de caracteres) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- concatenation
- +
- string
dev_langs:
- TSQL
helpviewer_keywords:
- concatenation [SQL Server]
- string concatenation operators
- + (string concatenation)
ms.assetid: 35cb3d7a-48f5-4b13-926c-a9d369e20ed7
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 66f482d424c6be56d89e8ec5b99cff30b2ddab0b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="-string-concatenation-transact-sql"></a>+ (Concatenação de cadeias de caracteres) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Um operador em uma expressão de cadeia de caracteres que concatena duas ou mais cadeias de caracteres ou cadeias de caracteres binárias, colunas ou uma combinação de cadeias de caracteres e nomes de colunas em uma expressão (um operador de cadeia de caracteres).  Por exemplo `SELECT 'book'+'case';` retorna `bookcase`.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression + expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos dados tipos caractere e categoria de tipo de dados binário, exceto o **imagem**, **ntext**, ou **texto**tipos de dados. As duas expressões devem ser do mesmo tipo de dados ou uma expressão deve poder ser convertida implicitamente no tipo de dados da outra expressão.  
  
 Uma conversão explícita em dados de caractere deve ser usada ao concatenar cadeias binárias e quaisquer caracteres entre as cadeias binárias. O exemplo a seguir mostra quando `CONVERT`, ou `CAST`, devem ser usados com concatenação binária e quando `CONVERT`, ou `CAST`, não precisa ser usado.  
  
```  
DECLARE @mybin1 varbinary(5), @mybin2 varbinary(5)  
SET @mybin1 = 0xFF  
SET @mybin2 = 0xA5  
-- No CONVERT or CAST function is required because this example   
-- concatenates two binary strings.  
SELECT @mybin1 + @mybin2  
-- A CONVERT or CAST function is required because this example  
-- concatenates two binary strings plus a space.  
SELECT CONVERT(varchar(5), @mybin1) + ' '   
   + CONVERT(varchar(5), @mybin2)  
-- Here is the same conversion using CAST.  
SELECT CAST(@mybin1 AS varchar(5)) + ' '   
   + CAST(@mybin2 AS varchar(5))  
  
```  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 O operador + (Concatenação de cadeias de caracteres) se comporta de maneira diferente ao trabalhar com uma cadeia de caracteres vazia de comprimento zero do que ao trabalhar com valores NULL ou desconhecidos. Uma cadeia de caracteres de comprimento zero pode ser especificada como duas aspas simples sem nenhum caractere dentro das aspas. Uma cadeia de caracteres binária de comprimento zero pode ser especificada como 0x sem nenhum valor de byte especificado na constante hexadecimal. A concatenação de uma cadeia de caracteres de comprimento zero sempre concatena as duas cadeias de caracteres especificadas. Quando você trabalhar com cadeias de caracteres com um valor nulo, o resultado da concatenação dependerá das configurações da sessão. Assim como as operações aritméticas que são executadas em valores nulos, quando um valor nulo é adicionado a um valor conhecido, o resultado normalmente será um valor desconhecido, uma operação de concatenação de cadeias de caracteres executada com um valor nulo também deve produzir um resultado nulo. No entanto, você pode alterar esse comportamento alterando a configuração de `CONCAT_NULL_YIELDS_NULL` para a sessão atual. Para obter mais informações, veja [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
 Se o resultado da concatenação de cadeias de caracteres exceder o limite de 8.000 bytes, o resultado será truncado. Entretanto, se pelo menos uma das cadeias de caracteres concatenadas for um tipo de valor grande, não ocorrerá truncamento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-string-concatenation"></a>A. Usando a concatenação de cadeias de caracteres  
 O exemplo a seguir cria uma única coluna sob o título de coluna `Name` a partir de colunas de vários caracteres, com o sobrenome da pessoa seguido por uma vírgula, um único espaço e o nome da pessoa. O conjunto de resultados está em ordem alfabética crescente pelo sobrenome e depois pelo nome.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM Person.Person  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="b-combining-numeric-and-date-data-types"></a>B. Combinando tipos de dados numéricos e de data  
 O exemplo a seguir usa o `CONVERT` função concatenar **numérico** e **data** tipos de dados.  
  
```  
-- Uses AdventureWorks  
  
SELECT 'The order is due on ' + CONVERT(varchar(12), DueDate, 101)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID = 50001;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------------------------------------------  
 The order is due on 04/23/2007  
 (1 row(s) affected)
 ```  
  
### <a name="c-using-multiple-string-concatenation"></a>C. Usando concatenação de várias cadeias de caracteres  
 O exemplo a seguir concatena várias cadeias de caracteres para formar uma cadeia de caracteres longa a fim de exibir o sobrenome e a primeira inicial dos vice-presidentes na [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]. Uma vírgula é adicionada depois do sobrenome e um ponto depois da primeira inicial.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ',' + SPACE(1) + SUBSTRING(FirstName, 1, 1) + '.') AS Name, e.JobTitle  
FROM Person.Person AS p  
    JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle LIKE 'Vice%'  
ORDER BY LastName ASC;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name               Title  
 -------------      ---------------`  
 Duffy, T.          Vice President of Engineering  
 Hamilton, J.       Vice President of Production  
 Welcker, B.        Vice President of Sales  

 (3 row(s) affected)
 ```  
 
### <a name="d-using-large-strings-in-concatenation"></a>D. Usando cadeias de caracteres grandes em concatenação
O exemplo a seguir concatena várias cadeias de caracteres para formar uma cadeia de caracteres longa e, em seguida, tenta calcular o comprimento da cadeia de caracteres final. O tamanho final do conjunto de resultados é 16000, porque é iniciado de avaliação de expressão da esquerda que é, @x + @z + @y = > (@x + @z) + @y. Nesse caso, o resultado de (@x + @z) são truncados em 8000 bytes e, em seguida, @y é adicionado ao conjunto de resultados, o que torna o comprimento da cadeia de caracteres final 16000. Como @y é uma cadeia de caracteres de tipo de valor grande, não ocorrerá truncamento.

```
DECLARE @x varchar(8000) = replicate('x', 8000)
DECLARE @y varchar(max) = replicate('y', 8000)
DECLARE @z varchar(8000) = replicate('z',8000)
SET @y = @x + @z + @y
-- The result of following select is 16000
SELECT len(@y) AS y
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 y        
 -------  
 16000  
  
 (1 row(s) affected)
 ```  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-string-concatenation"></a>E. Usando a concatenação de cadeias de caracteres  
 O exemplo a seguir cria uma única coluna sob o título de coluna `Name` das colunas de vários caracteres, com o sobrenome do contato seguido por uma vírgula, um único espaço e, em seguida, o nome do contato. O conjunto de resultados está em ordem alfabética crescente pelo sobrenome e depois pelo nome.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM DimEmployee  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="f-using-multiple-string-concatenation"></a>F. Usando concatenação de várias cadeias de caracteres  
 O exemplo a seguir concatena várias cadeias de caracteres para formar uma cadeia de caracteres longa para exibir o último nome e a primeira inicial dos vice-presidentes dentro de um banco de dados de exemplo. Uma vírgula é adicionada depois do sobrenome e um ponto depois da primeira inicial.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + SUBSTRING(FirstName, 1, 1) + '.') AS Name, Title  
FROM DimEmployee  
WHERE Title LIKE '%Vice Pres%'  
ORDER BY LastName ASC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name               Title                                           
-------------      ---------------  
Duffy, T.          Vice President of Engineering  
Hamilton, J.       Vice President of Production  
Welcker, B.        Vice President of Sales  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Conversão de tipo de dados &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [+ = &#40; Concatenação de cadeia de caracteres &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)  
  
  




