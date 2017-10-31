---
title: TRY_CAST (Transact-SQL) | Microsoft Docs
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
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09c5b6060798f28541f61e763954ed44920cf83d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="trycast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 O valor a ser convertido. Qualquer expressão válida.  
  
 *data_type*  
 O tipo de dados no qual converter *expressão*.  
  
 *length*  
 Inteiro opcional que especifica o comprimento do tipo de dados de destino.  
  
 O intervalo de valores aceitáveis é determinado pelo valor de *data_type*.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
## <a name="remarks"></a>Comentários  
 **TRY_CAST** usa o valor passado para ele e tenta convertê-lo em especificado *data_type*. Se a conversão for bem-sucedida, **TRY_CAST** retorna o valor conforme o especificado *data_type*; se ocorrer um erro, null será retornado. No entanto se você solicitar uma conversão que não é permitida explicitamente, em seguida, **TRY_CAST** falhará com um erro.  
  
 **TRY_CAST** não é uma palavra-chave reservada novo e está disponível em todos os níveis de compatibilidade. **TRY_CAST** tem a mesma semântica **TRY_CONVERT** ao se conectar a servidores remotos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-trycast-returns-null"></a>A. TRY_CAST retorna nulo  
 O exemplo a seguir demonstra que TRY_CAST retorna nulo quando a conversão falha.  
  
```tsql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
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
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-trycast-fails-with-an-error"></a>B. TRY_CAST falha com um erro  
 O exemplo a seguir demonstra que TRY_CAST retorna um erro quando a conversão não é permitida explicitamente.  
  
```tsql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 O resultado dessa instrução é um erro, porque um inteiro não pode ser convertido em um tipo de dados XML.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>C. TRY_CAST tem êxito  
 Este exemplo demonstra que a expressão deve estar no formato esperado.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
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
 [TRY_CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

