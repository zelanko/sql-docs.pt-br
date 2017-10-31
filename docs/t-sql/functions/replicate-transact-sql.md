---
title: REPLICATE (Transact-SQL) | Microsoft Docs
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
- REPLICATE_TSQL
- REPLICATE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], repeating
- REPLICATE function
- repeating character expressions
ms.assetid: 0cd467fb-3f22-471a-892c-0039d9f7fa1a
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2260073409ce6d7b558c65f2528f63423fdf1eb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="replicate-transact-sql"></a>REPLICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Repete um valor da cadeia de caracteres um número especificado de vezes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
REPLICATE ( string_expression ,integer_expression )   
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 É uma expressão de um tipo de dados binário ou cadeia de caracteres. *string_expression* pode ser um caractere ou dados binários.  
  
> [!NOTE]  
>  Se *string_expression* não é do tipo **varchar (max)** ou **nvarchar (max)**, REPLICATE truncará o valor de retorno em 8.000 bytes. Para retornar valores maiores que 8.000 bytes, *string_expression* devem ser explicitamente convertidos para o tipo de dados de valor grande apropriado.  
  
 *integer_expression*  
 É uma expressão de qualquer tipo de inteiro, incluindo **bigint**. Se *integer_expression* é negativa, NULL será retornado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o mesmo tipo *string_expression*.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-replicate"></a>A. Usando REPLICATE  
 O exemplo a seguir replica um caractere `0` quatro vezes na frente de um código de linha de produção no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT [Name]  
, REPLICATE('0', 4) + [ProductLine] AS 'Line Code'  
FROM [Production].[Product]  
WHERE [ProductLine] = 'T'  
ORDER BY [Name];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name                                               Line Code  
-------------------------------------------------- ---------  
HL Touring Frame - Blue, 46                        0000T   
HL Touring Frame - Blue, 50                        0000T   
HL Touring Frame - Blue, 54                        0000T   
HL Touring Frame - Blue, 60                        0000T   
HL Touring Frame - Yellow, 46                      0000T   
HL Touring Frame - Yellow, 50                      0000T  
...  
```  
  
### <a name="b-using-replicate-and-datalength"></a>B. Usando REPLICATE e DATALENGTH  
 O exemplo a seguir preenche números à esquerda até um comprimento especificado, à medida que são convertidos de um tipo de dados numérico em caractere ou Unicode.  
  
```  
IF EXISTS(SELECT name FROM sys.tables  
      WHERE name = 't1')  
   DROP TABLE t1;  
GO  
CREATE TABLE t1   
(  
 c1 varchar(3),  
 c2 char(3)  
);  
GO  
INSERT INTO t1 VALUES ('2', '2'), ('37', '37'),('597', '597');  
GO  
SELECT REPLICATE('0', 3 - DATALENGTH(c1)) + c1 AS 'Varchar Column',  
       REPLICATE('0', 3 - DATALENGTH(c2)) + c2 AS 'Char Column'  
FROM t1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Varchar Column        Char Column  
--------------------  ------------  
002                   2    
037                   37   
597                   597  
  
(3 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-replicate"></a>C: usando REPLICATE  
 O exemplo a seguir replica um `0` caractere quatro vezes na frente de um `ItemCode` valor.  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName AS Name,  
   ProductAlternateKey AS ItemCode,  
   REPLICATE('0', 4) + ProductAlternateKey AS FullItemCode  
FROM dbo.DimProduct  
ORDER BY Name;  
```  
  
 Aqui estão as primeiras linhas no conjunto de resultados.  
  
 ```
Name                     ItemCode       FullItemCode
------------------------ -------------- ---------------
Adjustable Race          AR-5381        0000AR-5381
All-Purpose Bike Stand   ST-1401        0000ST-1401
AWC Logo Cap             CA-1098        0000CA-1098
AWC Logo Cap             CA-1098        0000CA-1098
AWC Logo Cap             CA-1098        0000CA-1098
BB Ball Bearing          BE-2349        0000BE-2349
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


