---
title: Subcadeia de caracteres (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f36ec82c65e5d52c2186c67033adddbf1700c4d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna parte de uma expressão de caractere, binária, de texto ou de imagem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SUBSTRING (expressão, início, comprimento)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expressão*  
 É um **caractere**, **binário**, **texto**, **ntext**, ou **imagem** de [expressão](../../t-sql/language-elements/expressions-transact-sql.md). 
  
 *Início*  
 É um número inteiro ou **bigint** que especifica onde os caracteres retornados devem iniciar. (A numeração é 1 base, significando que o primeiro caractere da expressão é 1). Se *início* é menor que 1, a expressão retornada começará no primeiro caractere que é especificado em *expressão*. Nesse caso, o número de caracteres que são retornados é o maior valor de soma de *início* + *comprimento*- 1 ou 0. Se *início* é maior que o número de caracteres na expressão de valor, uma expressão de comprimento zero será retornada.  
  
 *Comprimento*  
 É um inteiro positivo ou **bigint** que especifica quantos caracteres da expressão de *expressão* serão retornados. Se o *comprimento* for negativo, um erro será gerado e a instrução será encerrada. Se a soma de *início* e *comprimento* for maior do que o número de caracteres em *expressão*, a expressão de valor inteiro, começando no *início*, será retornada.   
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna dados de caractere se *expressão* é um dos tipos de dados de caracteres com suporte. Retorna dados binários se *expressão* é um com suporte **binário** tipos de dados. A cadeia de caracteres retornada é do mesmo tipo que a expressão especificada com as exceções mostradas na tabela.  
  
|Expressão especificada|Tipo de retorno|  
|--------------------------|-----------------|  
|**char**/**varchar**/**texto**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binário**/**varbinary**/**imagem**|**varbinary**|  
  
## <a name="remarks"></a>Comentários  
 Os valores para *início* e *comprimento* devem ser especificados em número de caracteres para tipos de dados **ntext**, **char**, ou **varchar** e bytes para **texto**, **imagem**, **binário** ou **varbinary**.   
  
 A *expressão* deve ser **varchar (max)** ou **varbinary (max)** quando o *início* ou *comprimento* contém um valor maior que 2147483647.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 Ao usar agrupamentos de caracteres suplementares (SC), tanto *início* quanto *comprimento* contarão cada par substituto de *expressão* como um único caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).   
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-substring-with-a-character-string"></a>A. Usando SUBSTRING com uma cadeia de caracteres  
 O exemplo a seguir mostra como retornar somente uma parte de uma cadeia de caracteres. Na tabela `sys.databases`, esta consulta retorna os nomes dos bancos de dados do sistema na primeira coluna, a primeira letra do banco de dados na segunda coluna e o terceiro e o quarto caracteres na coluna final.   
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|nome |Initial |ThirdAndFourthCharacters|
|---|--|--|
|mestre  |m  |st |
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
>  Para executar os exemplos a seguir, você deve instalar o **pubs** banco de dados.  
  
 O exemplo a seguir mostra como retornar os 10 primeiros caracteres de cada coluna de dados de **texto** e **imagem** na tabela `pub_info`do banco de dados `pubs`. Os dados de **texto** são retornados como **varchar** e os dados de **imagem** são retornadas como **varbinary**.  
  
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
  
 O exemplo a seguir mostra o efeito de SUBSTRING em ambos os tipos de dado **texto** e **ntext**. Primeiro, este exemplo cria uma nova tabela no banco de dados `pubs` chamado `npub_info`. Depois, o exemplo cria a coluna `pr_info` na tabela `npub_info` com os primeiros 80 caracteres da coluna `pub_info.pr_info` e adiciona um `ü` como o primeiro caractere. Por fim, um `INNER JOIN` recupera todos os números de identificação de publicador e o `SUBSTRING` de ambos os **texto** e **ntext** colunas de informações do publicador.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
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
  
 O exemplo a seguir mostra como retornar o segundo, terceiro e quarto caracteres da constante de cadeia de caracteres `abcdef`.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



