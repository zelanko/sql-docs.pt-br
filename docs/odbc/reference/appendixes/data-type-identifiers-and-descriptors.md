---
title: Identificadores e descritores de tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f65bc86213f99112daf17c67a4ca522490d32149
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284479"
---
# <a name="data-type-identifiers-and-descriptors"></a>Identificadores e descritores de tipo de dados
Os tipos de dados listados nas seções [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) e [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) , anteriormente neste apêndice, são tipos de dados "concisos": cada identificador refere-se a um único tipo de dados. Há uma correspondência um-para-um entre o identificador e o tipo de dados. Os descritores, no entanto, não em todos os casos usam um único valor para identificar tipos de dados. Em alguns casos, eles usam um tipo de dados "detalhado" e um subcódigo de tipo. Para todos os tipos de dados, exceto os tipos de dados DateTime e Interval, o identificador de tipo detalhado é o mesmo que o identificador de tipo conciso e o valor em SQL_DESC_DATETIME_INTERVAL_CODE é igual a 0. No entanto, para os tipos de dados DateTime e Interval, um tipo Detalhado (SQL_DATETIME ou SQL_INTERVAL) é armazenado em SQL_DESC_TYPE, um tipo conciso é armazenado em SQL_DESC_CONCISE_TYPE e um subcódigo para cada tipo conciso é armazenado em SQL_DESC_DATETIME_INTERVAL_CODE. Definir um desses campos afeta os outros. Para obter mais informações sobre esses campos, consulte a descrição da função [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) .  
  
 Quando o campo SQL_DESC_TYPE ou SQL_DESC_CONCISE_TYPE é definido para alguns tipos de dados, os campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_SCALE são automaticamente definidos como valores padrão, conforme aplicável ao tipo de dados. Para obter mais informações, consulte a descrição do campo SQL_DESC_TYPE em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Se qualquer um dos valores padrão definidos não for apropriado, o aplicativo deverá definir explicitamente o campo de descritor por meio de uma chamada para **SQLSetDescField**.  
  
 A tabela a seguir mostra o identificador de tipo conciso, o identificador de tipo detalhado, e o subcódigo de tipo de cada DateTime e o identificador de tipo SQL e C. Como essa tabela indica, para os tipos de dados DateTime e Interval, os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE têm as mesmas constantes de manifesto para tipos de dados SQL (em descritores de implementação) e para tipos de dados C (em descritores de aplicativo).  
  
|Tipo SQL conciso|Tipo C conciso|Tipo detalhado|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
