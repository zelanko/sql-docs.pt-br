---
title: NCHAR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- nchar
- nchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NCHAR function
- Unicode [SQL Server], NCHAR function
ms.assetid: 68cefc68-7c4f-4326-80c1-300f90cf19db
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: b70c591517177ad9febd1d0d9873a41192bf9414
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="nchar-transact-sql"></a>NCHAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o caractere Unicode com o código inteiro especificado, como definido pelo padrão do Unicode.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
NCHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression*  
 Quando o agrupamento do banco de dados não contiver o sinalizador de caractere suplementar (SC), esse será um número inteiro positivo de 0 a 65535 (0 a 0xFFFF). Se for especificado um valor fora deste intervalo, será retornado NULL. Para obter mais informações sobre caracteres suplementares, consulte [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 Quando o agrupamento do banco de dados não oferecer suporte ao sinalizador de caractere suplementar (SC), esse será um número inteiro positivo de 0 a 1114111 (0 a 0x10FFFF). Se for especificado um valor fora deste intervalo, será retornado NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nchar (1)** quando o agrupamento de banco de dados padrão não oferece suporte a caracteres suplementares.  
  
 **nvarchar(2)** quando o agrupamento de banco de dados padrão oferece suporte a caracteres suplementares.  
  
 Se o parâmetro *integer_expression* estiver no intervalo 0 - 0xFFFF, somente um caractere será retornado. Para valores mais altos, NCHAR retorna o par alternativo correspondente. Não construa um par alternativo usando `NCHAR(<High surrogate>) + NCHAR(\<Low Surrogate>)`. Em vez disso, use um agrupamento de banco de dados com suporte para caracteres suplementares e especifique o ponto de código Unicode para o par substituto. O exemplo a seguir demonstra o método de estilo antigo de construir um par substituto e o método preferencial de especificar o ponto de código Unicode.  
  
```  
CREATE DATABASE test COLLATE Finnish_Swedish_100_CS_AS_SC;  
DECLARE @d nvarchar(10) = N'ࣅ炙   
-– Old style method.  
SELECT NCHAR(0xD84C) + NCHAR(0xDD7F);   
  
-- Preferred method.   
SELECT NCHAR(143743);   
  
-- Alternative preferred method.  
SELECT NCHAR(UNICODE(@d));    
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-nchar-and-unicode"></a>A. Usando NCHAR e UNICODE  
 O exemplo a seguir usa as funções `UNICODE` e `NCHAR` para imprimir o valor `UNICODE` e o `NCHAR` (caractere Unicode) do segundo caractere da cadeia de caracteres `København` e para imprimir o segundo caractere real, `ø`.  
  
```  
DECLARE @nstring nchar(8);  
SET @nstring = N'København';  
SELECT UNICODE(SUBSTRING(@nstring, 2, 1)),   
   NCHAR(UNICODE(SUBSTRING(@nstring, 2, 1)));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
248         ø  
(1 row(s) affected)  
```  
  
### <a name="b-using-substring-unicode-convert-and-nchar"></a>B. Usando SUBSTRING, UNICODE, CONVERT e NCHAR  
 O exemplo a seguir usa as funções `SUBSTRING`, `UNICODE`, `CONVERT` e `NCHAR` para imprimir o número do caractere, o caractere Unicode e o valor UNICODE de cada caractere na cadeia `København`.  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(9);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.  
-- Notice that there is an N before the start of the string. This   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'København';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
   BEGIN  
   SELECT @position,   
      NCHAR(UNICODE(SUBSTRING(@nstring, @position, 1))),  
      CONVERT(NCHAR(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1))  
   SELECT @position = @position + 1  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ---- ----------------- -----------   
1           K    K                 75  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
2           ø    ø                 248  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
3           b    b                 98  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
4           e    e                 101  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
5           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
6           h    h                 104  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
7           a    a                 97  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
8           v    v                 118  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
9           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
10          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
11          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
12          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
13          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
14          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
15          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
16          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
17          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
18          NULL                   NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [UNICODE &#40; Transact-SQL &#41;](../../t-sql/functions/unicode-transact-sql.md)  
  
  


