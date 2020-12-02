---
description: Operadores bit a bit (Transact-SQL)
title: Operadores bit a bit (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 15649f0ff6a9695b17af629f28156ea4860e4aa6
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128320"
---
# <a name="bitwise-operators-transact-sql"></a>Operadores bit a bit (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Os operadores bit a bit desempenham manipulações de bit entre duas expressões de qualquer um dos tipos de dados da categoria de tipo de dados inteiro.  
  Os operadores bit a bit convertem dois valores inteiros em bits binários, executam a operação AND, OR ou NOT em cada bit, produzindo um resultado. Em seguida, eles convertem o resultado em um inteiro.  
  
  Por exemplo, o inteiro 170 é convertido em 1010 1010 binário.
O inteiro 75 é convertido em 0100 1011 binário.

|operador|matemática bit a bit|
|---- |---- |
|AND <br> Se os bits em qualquer local forem 1, o resultado será 1. |1010 1010 = 170 <br>0100 1011 = 75 <br>-----------------  <br> 0000 1010 = 10 |
|OU <br> Se um dos bits em qualquer local for 1, o resultado será 1. |1010 1010 = 170 <br>0100 1011 = 75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> Reverte o valor de bit em cada local de bit. |1010 1010 = 170 <br>----------------- <br>  0101 0101 = 85 |
  
Consulte os seguintes tópicos:   
* [& &#40;AND bit a bit&#41;](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [&= &#40;Atribuição de AND bit a bit&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124; &#40;OR bit a bit&#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124;= &#40;Atribuição de OR bit a bit&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ &#40;OR exclusivo bit a bit&#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^= &#40;Atribuição de OR exclusivo bit a bit&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ &#40;NOT bit a bit&#41;](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 Os operandos dos operadores bit a bit podem ser um dos tipos de dados das categorias de tipo de dados inteiro ou cadeia de caracteres binária (exceto o tipo de dados **image**), mas os operadores não podem ser um dos tipos de dados da categoria de tipo de dados de cadeia de caracteres binária. A tabela a seguir mostra os tipos de dados de operando com suporte.  
  
|Operando da esquerda|Operando da direita|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint** ou **tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**, **smallint**, **tinyint** ou **bits**|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**bigint**, **int**, **smallint**, **tinyint**, **binary** ou **varbinary**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** ou **varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** ou **varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binary** ou **varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint** ou **tinyint**|  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)
