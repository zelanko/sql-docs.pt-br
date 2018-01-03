---
title: Identificadores e descritores de tipo de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f54638aa02c885ee0e6fe8d14310d319dafb11c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="data-type-identifiers-and-descriptors"></a>Identificadores de tipo de dados e descritores
Os tipos de dados listados no [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) e [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) seções anteriores neste apêndice são tipos de dados "concisa": cada identificador se refere a um único tipo de dados. Não há uma correspondência entre o identificador e o tipo de dados. Descritores de, no entanto, fazer não em todos os casos a usar um único valor para identificar os tipos de dados. Em alguns casos, eles usam um tipo de dados "detalhados" e um subcódigo de tipo. Para todos os tipos de dados, exceto os tipos de dados de data e hora e intervalo, o identificador de tipo detalhado é o mesmo que o identificador de tipo concisa e o valor em SQL_DESC_DATETIME_INTERVAL_CODE é igual a 0. Para tipos de dados de data e hora e intervalo, no entanto, um tipo detalhado (SQL_DATETIME ou SQL_INTERVAL) é armazenado em SQL_DESC_TYPE, um tipo conciso é armazenado em SQL_DESC_CONCISE_TYPE e um subcódigo para cada tipo conciso é armazenado em SQL_DESC_DATETIME_INTERVAL_CODE. A configuração de um desses campos afeta os outros. Para obter mais informações sobre esses campos, consulte o [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) descrição da função.  
  
 Quando o campo SQL_DESC_TYPE ou SQL_DESC_CONCISE_TYPE é definido para alguns tipos de dados, os campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_SCALE, SQL_DESC_PRECISION e SQL_DESC_LENGTH são definidos automaticamente como valores padrão, conforme aplicável para os dados tipo. Para obter mais informações, consulte a descrição do campo SQL_DESC_TYPE em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Se qualquer um dos valores padrão não for apropriado, o aplicativo deve definir explicitamente por meio de uma chamada para o campo do descritor **SQLSetDescField**.  
  
 A tabela a seguir mostra o identificador de tipo concisa, identificador de tipo detalhado e subcódigo de tipo para cada data e hora e o intervalo de SQL e o identificador de tipo C. Como esta tabela indica, para tipos de dados de data e hora e intervalo, os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE têm as mesmo constantes de manifesto para tipos de dados SQL (em descritores de implementação) e tipos de dados C (no aplicativo descritores).  
  
|Um tipo SQL|Um tipo de C|Tipo detalhado|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
QL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
QL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
