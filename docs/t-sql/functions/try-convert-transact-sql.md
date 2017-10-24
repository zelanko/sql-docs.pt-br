---
title: TRY_CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0cb3854ae349b17dcdb0b0528c6415fd41b1e072
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_type [(comprimento)]*  
 O tipo de dados no qual converter *expressão*.  
  
 *expressão*  
 O valor a ser convertido.  
  
 *estilo*  
 Expressão de inteiro opcional que especifica como o **TRY_CONVERT** função é converter *expressão*.  
  
 *estilo* aceita os mesmos valores que o *estilo* parâmetro o **converter** função. Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 O intervalo de valores aceitáveis é determinado pelo valor de *data_type*. Se *estilo* for nulo, **TRY_CONVERT** retorna nulo.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
## <a name="remarks"></a>Comentários  
 **TRY_CONVERT** usa o valor passado para ele e tenta convertê-lo em especificado *data_type*. Se a conversão for bem-sucedida, **TRY_CONVERT** retorna o valor conforme o especificado *data_type*; se ocorrer um erro, null será retornado. No entanto se você solicitar uma conversão que não é permitida explicitamente, em seguida, **TRY_CONVERT** falhará com um erro.  
  
 **TRY_CONVERT** é uma palavra reservada no nível de compatibilidade 110 e superior.  
  
 Essa função é capaz de ser remota para servidores da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior. Ela não será remota para servidores que têm uma versão anterior ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-tryconvert-returns-null"></a>A. TRY_CONVERT retorna nulo  
 O exemplo a seguir demonstra que TRY_CONVERT retorna nulo quando a conversão falha.  
  
```tsql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 O exemplo a seguir demonstra que a expressão deve estar no formato esperado.  
  
```tsql  
SET DATEFORMAT dmy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-tryconvert-fails-with-an-error"></a>B. TRY_CONVERT falha com um erro  
 O exemplo a seguir demonstra que TRY_CONVERT retorna um erro quando a conversão não é permitida explicitamente.  
  
```tsql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 O resultado dessa instrução é um erro, porque um inteiro não pode ser convertido em um tipo de dados XML.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-tryconvert-succeeds"></a>C. TRY_CONVERT bem-sucedido  
 Este exemplo demonstra que a expressão deve estar no formato esperado.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

