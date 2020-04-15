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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284479"
---
# <a name="data-type-identifiers-and-descriptors"></a>Identificadores e descritores de tipo de dados
Os tipos de dados listados nas seções [SQL Data Types](../../../odbc/reference/appendixes/sql-data-types.md) and [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) anteriormente neste apêndice são tipos de dados "concisos": Cada identificador refere-se a um único tipo de dados. Há uma correspondência um-para-um entre o identificador e o tipo de dados. Os descritores, no entanto, não usam em todos os casos um único valor para identificar tipos de dados. Em alguns casos, eles usam um tipo de dados "verboso" e um subcódigo de tipo. Para todos os tipos de dados, exceto os tipos de dados de data e intervalo, o identificador de tipo verbose é o mesmo que o identificador de tipo conciso e o valor em SQL_DESC_DATETIME_INTERVAL_CODE é igual a 0. No entanto, para os tipos de dados de data e intervalo, um tipo de verbosa (SQL_DATETIME ou SQL_INTERVAL) é armazenado em SQL_DESC_TYPE, um tipo conciso é armazenado em SQL_DESC_CONCISE_TYPE e um subcódigo para cada tipo conciso é armazenado em SQL_DESC_DATETIME_INTERVAL_CODE. Definir um desses campos afeta os outros. Para obter mais informações sobre esses campos, consulte a descrição da função [SQLSetDescField.](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
 Quando o campo SQL_DESC_TYPE ou SQL_DESC_CONCISE_TYPE é definido para alguns tipos de dados, os campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_SCALE são automaticamente definidos como valores padrão, conforme aplicável para o tipo de dados. Para obter mais informações, consulte a descrição do campo SQL_DESC_TYPE em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Se algum dos valores padrão definido não for apropriado, o aplicativo deve definir explicitamente o campo descritor através de uma chamada para **SQLSetDescField**.  
  
 A tabela a seguir mostra o identificador de tipo conciso, o identificador de tipo verbose e o subcódigo de tipo para cada identificador de tipo SQL e C de data e intervalo. Como esta tabela indica, para os tipos de dados de data e intervalo, os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE têm as mesmas constantes de manifesto tanto para os tipos de dados SQL (em descritores de implementação) quanto para os tipos de dados C (em descritores de aplicativos).  
  
|Tipo SQL conciso|Tipo C conciso|Tipo verbose|DATETIME_INTERVAL_CODE|  
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
