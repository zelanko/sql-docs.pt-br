---
title: O conjunto de resultados SQLGetTypeInfo de exemplo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8264f1dfad8bff5d676cd4de8c8b9d7763b39b52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948741"
---
# <a name="example-sqlgettypeinfo-result-set"></a>Conjunto de resultados SQLGetTypeInfo de exemplo
Um aplicativo chama **SQLGetTypeInfo** para determinar quais tipos de dados são compatíveis com uma fonte de dados e as características desses tipos de dados. As tabelas a seguir mostram um conjunto de resultados de exemplo retornado por **SQLGetTypeInfo** para uma fonte de dados que dá suporte a SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR e SQL_INTERVAL_DAY_TO_SECOND.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"char"|SQL_CHAR|255|"'"|"'"|"comprimento"|SQL_TRUE|  
|"texto"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<NULL >|SQL_TRUE|  
|"decimal"|SQL_DECIMAL|28|\<NULL >|\<NULL >|"precisão,<br />escala"|SQL_TRUE|  
|"real"|SQL_REAL|7|\<NULL >|\<NULL >|\<NULL >|SQL_TRUE|  
|"datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<NULL >|SQL_TRUE|  
|"INTERVALO YEAR() AO ANO"|SQL_INTERVAL_YEAR|9|"'"|"'"|"precisão"|SQL_TRUE|  
|"INTERVALO DAY() PARA FRACTION(5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"precisão"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<NULL >|SQL_FALSE|\<NULL >|"char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<NULL >|SQL_FALSE|\<NULL >|"texto"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"decimal"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"real"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<NULL >|SQL_FALSE|\<NULL >|"datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<NULL >|SQL_FALSE|\<NULL >|"INTERVALO YEAR() AO ANO"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<NULL >|SQL_FALSE|\<NULL >|"INTERVALO DAY() PARA FRACTION(5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<NULL >|\<NULL >|SQL_CHAR|\<NULL >|\<NULL >|\<NULL >|  
|**SQL_LONGVARCHAR**|\<NULL >|\<NULL >|SQL_LONGVARCHAR|\<NULL >|\<NULL >|\<NULL >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<NULL >|10|\<NULL >|  
|**SQL_REAL**|\<NULL >|\<NULL >|SQL_REAL|\<NULL >|10|\<NULL >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<NULL >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<NULL >|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<NULL >|9|
