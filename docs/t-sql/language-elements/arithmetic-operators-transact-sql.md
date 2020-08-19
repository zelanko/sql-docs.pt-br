---
description: Operadores aritméticos (Transact-SQL)
title: Operadores aritméticos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b51c473bb75f3f2e1c82f96dcd8af743597678fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445513"
---
# <a name="arithmetic-operators-transact-sql"></a>Operadores aritméticos (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Os operadores aritméticos executam operações matemáticas em duas expressões de um ou mais tipos de dados. Eles são executados da categoria de tipo de dados numéricos. Para obter mais informações sobre as categorias de tipo de dados, confira [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Operador|Significado|  
|--------------|-------------|  
|[+ (Somar)](../../t-sql/language-elements/add-transact-sql.md)|Adição|  
|[- (Subtrair)](../../t-sql/language-elements/subtract-transact-sql.md)|Subtração|  
|[* (Multiplicar)](../../t-sql/language-elements/multiply-transact-sql.md)|Multiplicação|  
|[/ (dividir)](../../t-sql/language-elements/divide-transact-sql.md)|Divisão|  
|[% (módulo)](../../t-sql/language-elements/modulo-transact-sql.md)|Retorna o resto inteiro de uma divisão. Por exemplo, 12% 5 = 2 porque o resto de 12 dividido por 5 é 2.|  
  
Os operadores de adição (+) e de subtração (-) também podem ser usados para executar operações aritméticas em valores de **datetime** e **smalldatetime**.  
  
Confira mais informações sobre a precisão e a escala de um resultado de operação aritmética em [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
