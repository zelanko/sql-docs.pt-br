---
title: TRY_CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0246c445565303eb3ad7fa170bf38c6f40bf18fe
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782357"
---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_type [ ( length ) ]*  
 O tipo de dados no qual converter *expression*.  
  
 *expressão*  
 O valor a ser convertido.  
  
 *style*  
 Expressão de inteiro opcional que especifica como a função **TRY_CONVERT** deve converter *expression*.  
  
 *style* aceita os mesmos valores do parâmetro *style* da função **CONVERT**. Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 O intervalo de valores aceitáveis é determinado pelo valor de *data_type*. Se *style* for nulo, **TRY_CONVERT** retornará nulo.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
## <a name="remarks"></a>Remarks  
 **TRY_CONVERT** usa o valor passado a ele e tenta convertê-lo no *data_type* especificado. Se a conversão for bem-sucedida, **TRY_CONVERT** retornará o valor como o *data_type* especificado; se ocorrer um erro, será retornado nulo. Porém, se você solicitar uma conversão que não é permitida explicitamente, **TRY_CONVERT** falhará com um erro.  
  
 **TRY_CONVERT** é uma palavra-chave reservada no nível de compatibilidade 110 e superior.  
  
 Essa função é capaz de ser remota para servidores da versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior. Ela não será remota para servidores que têm uma versão anterior ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-tryconvert-returns-null"></a>A. TRY_CONVERT retorna nulo  
 O exemplo a seguir demonstra que TRY_CONVERT retorna nulo quando a conversão falha.  
  
```sql  
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
  
```sql  
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
  
```sql  
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
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
