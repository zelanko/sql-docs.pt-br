---
title: SUBSTRING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 429be4403d1df512b43a049b0014afcafea15740
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947496"
---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna parte de uma expressão de caractere, binária, de texto ou de imagem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É **character**, **binary**, **text**, **ntext**ou **image**[expression](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *start*  
 É um inteiro ou uma expressão **bigint** que especifica o ponto em que os caracteres retornados devem iniciar. (A numeração é baseada em 1, ou seja, o primeiro caractere da expressão é 1). Se *start* for menos que 1, a expressão retornada começará no primeiro caractere especificado em *expression*. Nesse caso, o número de caracteres retornados é o valor maior da soma de *start* + *length*- 1 ou 0. Se *start* for maior que o número de caracteres na expressão de valor, uma expressão de comprimento zero será retornada.  
  
 *length*  
 É um inteiro positivo ou uma expressão **bigint** que especifica quantos caracteres da *expression* são retornados. Se *lenght* for negativo, um erro será gerado e a instrução será encerrada. Se a soma de *start* e *length* for maior que o número de caracteres em *expression*, a expressão de valor inteiro, começando no *start* será retornado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna dados de caractere se *expression* é um dos tipos de dados de caractere compatíveis. Retorna dados binários se *expression* é um dos tipos de dados **binary** compatíveis. A cadeia de caracteres retornada é do mesmo tipo que a expressão especificada com as exceções mostradas na tabela.  
  
|Expressão especificada|Tipo de retorno|  
|--------------------------|-----------------|  
|**char**/**varchar**/**text**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binary**/**varbinary**/**image**|**varbinary**|  
  
## <a name="remarks"></a>Remarks  
 Os valores para *start* e *length* devem ser especificados em número de caracteres para tipos de dados **ntext**, **char** ou **varchar** e bytes para tipos de dados **text**, **image**, **binary** ou **varbinary**.  
  
 A *expression* devem ser **varchar(max)** ou **varbinary(max)** quando o *start* ou *length* contém um valor maior que 2147483647.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 Ao usar ordenações de caracteres suplementares (SC), tanto *start* quanto *length* contarão cada par alternativo na *expression* como um único caractere. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-substring-with-a-character-string"></a>A. Usando SUBSTRING com uma cadeia de caracteres  
 O exemplo a seguir mostra como retornar somente uma parte de uma cadeia de caracteres. Na tabela `sys.databases`, esta consulta retorna os nomes do banco de dados do sistema na primeira coluna, a primeira letra do banco de dados na segunda coluna e os terceiros e quarto caracteres na coluna final.  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|NAME |Inicial |ThirdAndFourthCharacters|
|---|--|--|
|master  |m  |st |
|tempdb  |t  |mp |
|modelo   |m  |de |
|msdb    |m  |db |


  
 Veja como exibir o segundo, terceiro e quarto caracteres da constante de cadeia de caracteres `abcdef`.  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x  
----------  
bcd  
  
(1 row(s) affected)
```  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. Usando SUBSTRING com dados de texto, ntext e de imagem  
  
> [!NOTE]  
>  Para executar os exemplos a seguir, é necessário instalar o banco de dados **pubs**.  
  
 O exemplo a seguir mostra como retornar os 10 primeiros caracteres de cada coluna de dados **text** e **image** na tabela `pub_info` do banco de dados `pubs`. Dados de **text** são retornados como **varchar**, e dados de **image** são retornados como **varbinary**.  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 pub_id logo    pr_info
------ ---------------------- ----------
1756   0x474946383961E3002500 This is sa

(1 row(s) affected)
```  
  
 O exemplo a seguir mostra o efeito de SUBSTRING em dados **text** e **ntext**. Primeiro, este exemplo cria uma nova tabela no banco de dados `pubs` chamado `npub_info`. Depois, o exemplo cria a coluna `pr_info` na tabela `npub_info` com os primeiros 80 caracteres da coluna `pub_info.pr_info` e adiciona um `ü` como o primeiro caractere. Por último, um `INNER JOIN` recupera todos os números de identificação de editor e a `SUBSTRING` das colunas de informações de editor **text** e **ntext**.  
  
```  
IF EXISTS (SELECT table_name FROM INFORMATION_SCHEMA.TABLES   
      WHERE table_name = 'npub_info')  
   DROP TABLE npub_info;  
GO  
-- Create npub_info table in pubs database. Borrowed from instpubs.sql.  
USE pubs;  
GO  
CREATE TABLE npub_info  
(  
 pub_id char(4) NOT NULL  
    REFERENCES publishers(pub_id)  
    CONSTRAINT UPKCL_npubinfo PRIMARY KEY CLUSTERED,  
pr_info ntext NULL  
);  
  
GO  
  
-- Fill the pr_info column in npub_info with international data.  
RAISERROR('Now at the inserts to pub_info...',0,1);  
  
GO  
  
INSERT npub_info VALUES('0736', N'üThis is sample text data for New Moon Books, publisher 0736 in the pubs database')  
,('0877', N'üThis is sample text data for Binnet & Hardley, publisher 0877 in the pubs databa')  
,('1389', N'üThis is sample text data for Algodata Infosystems, publisher 1389 in the pubs da')  
,('9952', N'üThis is sample text data for Scootney Books, publisher 9952 in the pubs database')  
,('1622', N'üThis is sample text data for Five Lakes Publishing, publisher 1622 in the pubs d')  
,('1756', N'üThis is sample text data for Ramona Publishers, publisher 1756 in the pubs datab')  
,('9901', N'üThis is sample text data for GGG&G, publisher 9901 in the pubs database. GGG&G i')  
,('9999', N'üThis is sample text data for Lucerne Publishing, publisher 9999 in the pubs data');  
GO  
-- Join between npub_info and pub_info on pub_id.  
SELECT pr.pub_id, SUBSTRING(pr.pr_info, 1, 35) AS pr_info,  
   SUBSTRING(npr.pr_info, 1, 35) AS npr_info  
FROM pub_info pr INNER JOIN npub_info npr  
   ON pr.pub_id = npr.pub_id  
ORDER BY pr.pub_id ASC;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-substring-with-a-character-string"></a>C. Usando SUBSTRING com uma cadeia de caracteres  
 O exemplo a seguir mostra como retornar somente uma parte de uma cadeia de caracteres. Da tabela `dbo.DimEmployee`, essa consulta retorna o sobrenome em uma coluna com apenas a primeira inicial na segunda coluna.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName             Initial
-------------------- -------
Barbariol            A
Barber               D
Barreto de Mattos    P
```  
  
 O exemplo a seguir mostra como retornar o segundo, o terceiro e o quarto caracteres da constante de cadeia de caracteres `abcdef`.  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x
-----
bcd
```  
  
## <a name="see-also"></a>Consulte Também  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


