---
description: UNICODE (Transact-SQL)
title: UNICODE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UNICODE
- UNICODE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first character of input expression [SQL Server]
- UNICODE function
- Unicode [SQL Server], UNICODE function
ms.assetid: 5e3c40b2-8401-4741-9f2a-bae70eaa4da6
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 273faa70282ca1bc9c6ec0ab441dcb5f6fcfda1a
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990186"
---
# <a name="unicode-transact-sql"></a>UNICODE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o valor inteiro, como definido pelo padrão Unicode, para o primeiro caractere da expressão de entrada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
UNICODE ( 'ncharacter_expression' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
**'** *ncharacter_expression* **'**  
É uma expressão **nchar** ou **nvarchar**.  
  
## <a name="return-types"></a>Tipos de retorno  
**int**  
  
## <a name="remarks"></a>Comentários  
Nas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], a função UNICODE retorna um ponto de código UCS-2 no intervalo de 000000 a 00FFFF que pode representar os 65.535 caracteres em BMP (Plano Multilíngue Básico) em Unicode. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], ao usar ordenações habilitadas por [Caractere Suplementar (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters), o UNICODE retorna um ponto de código UTF-16 no intervalo de 000000 a 10FFFF. Para saber mais sobre o suporte a Unicode em [!INCLUDE[ssde_md](../../includes/ssde_md.md)], confira [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn). 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>a. Usando UNICODE e a função NCHAR  
 O exemplo a seguir usa as funções `UNICODE` e `NCHAR` para imprimir o valor UNICODE do primeiro caractere da cadeia de 24 caracteres `Åkergatan` e para imprimir o primeiro caractere real, `Å`.  
  
```sql  
DECLARE @nstring nchar(12);  
SET @nstring = N'Åkergatan 24';  
SELECT UNICODE(@nstring), NCHAR(UNICODE(@nstring));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
197         Å  
```  
  
### <a name="b-using-substring-unicode-and-convert"></a>B. Usando SUBSTRING, UNICODE e CONVERT  
 O exemplo a seguir usa as funções `SUBSTRING`, `UNICODE` e `CONVERT` para imprimir o número do caractere, o caractere Unicode e o valor UNICODE de cada um dos caracteres na cadeia `Åkergatan 24`.  
  
```sql  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(12);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.   
-- Notice that there is an N before the start of the string, which   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'Åkergatan 24';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= LEN(@nstring)  
-- While these are still characters in the character string,  
BEGIN;  
   SELECT @position AS [position],   
      SUBSTRING(@nstring, @position, 1) AS [character],  
      UNICODE(SUBSTRING(@nstring, @position, 1)) AS [code_point];  
   SET @position = @position + 1;  
END; 
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ----------------- -----------   
1           Å                 197           
  
----------- ----------------- -----------   
2           k                 107           
  
----------- ----------------- -----------   
3           e                 101           
  
----------- ----------------- -----------   
4           r                 114           
  
----------- ----------------- -----------   
5           g                 103           
  
----------- ----------------- -----------   
6           a                 97            
  
----------- ----------------- -----------   
7           t                 116           
  
----------- ----------------- -----------   
8           a                 97            
  
----------- ----------------- -----------   
9           n                 110           
  
----------- ----------------- -----------   
10                            32            
  
----------- ----------------- -----------   
11          2                 50            
  
----------- ----------------- -----------   
12          4                 52  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ASCII &#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [CHAR &#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

