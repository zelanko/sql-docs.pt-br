---
title: TRY_CAST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016 ||>= sql-server-linux-2017||= sqlallproducts-allversions||>= aps-pdw-2016||= azure-sqldw-latest
ms.openlocfilehash: 915ea023442ab9d787a481cab44259b1fc4a3857
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70151950"
---
# <a name="try_cast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 O valor a ser convertido. Qualquer expressão válida.  
  
 *data_type*  
 O tipo de dados no qual converter *expression*.  
  
 *length*  
 Inteiro opcional que especifica o comprimento do tipo de dados de destino.  
  
 O intervalo de valores aceitáveis é determinado pelo valor de *data_type*.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna uma conversão de valor ao tipo de dados especificado se a conversão for bem-sucedida; caso contrário, retorna nulo.  
  
## <a name="remarks"></a>Comentários  
 **TRY_CAST** usa o valor passado para ele e tenta convertê-lo no *data_type* especificado. Se a conversão for bem-sucedida, **TRY_CAST** retornará o valor como o *data_type* especificado; se um erro ocorrer, será retornado um valor nulo. Porém, se você solicitar uma conversão que não é permitida explicitamente, **TRY_CAST** falhará com um erro.  
  
 **TRY_CAST** não é uma nova palavra-chave reservada e está disponível em todos os níveis de compatibilidade. **TRY_CAST** tem a mesma semântica de **TRY_CONVERT** ao se conectar a servidores remotos.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-try_cast-returns-null"></a>a. TRY_CAST retorna nulo  
 O exemplo a seguir demonstra que TRY_CAST retorna nulo quando a conversão falha.  
  
```sql  
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
  
```sql  
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
  
### <a name="b-try_cast-fails-with-an-error"></a>B. TRY_CAST falha com um erro  
 O exemplo a seguir demonstra que TRY_CAST retorna um erro quando a conversão não é permitida explicitamente.  
  
```sql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 O resultado dessa instrução é um erro, porque um inteiro não pode ser convertido em um tipo de dados XML.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-try_cast-succeeds"></a>C. TRY_CAST tem êxito  
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
  
## <a name="see-also"></a>Consulte Também  
 [TRY_CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
