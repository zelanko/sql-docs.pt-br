---
title: Metadados do catálogo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
- catalog metadata [ODBC]
ms.assetid: b82665be-8cb1-4ad3-ac15-2e590bdc1815
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2784b7915d96665cae814e0dff46b2f2135bc52
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62511520"
---
# <a name="catalog-metadata"></a>Metadados de catálogo
  Este tópico descreve os metadados de coluna retornados por `SQLColumns` e `SQLProcedureColumns`, além dos metadados de tipo de dados retornados por `SQLGetTypeInfo`.  
  
## <a name="remarks"></a>Comentários  
 Os valores de coluna a seguir são retornados para tipos de data/hora por `SQLColumns` e `SQLProcedureColumns`:  
  
|Tipo de parâmetro|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8, 10.. 16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|6|10|16|16|16|20|  
|DECIMAL_DIGITS|0|0..7|0|3|1.. 7|1.. 7|  
|SQL_DATA_TYPE|SQL_DATETIME|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TYPE_TIMESTAMPOFFSET|  
|SQL_DATETIME_SUB|SQL_CODE_DATE|NULO|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULO|  
|CHAR_OCTET_LENGTH|NULO|NULO|NULO|NULO|NULO|NULO|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 Os valores de coluna a seguir são retornados para tipos de data/hora por `SQLGetTypeInfo`:  
  
|Tipo de parâmetro|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULO|scale|NULO|NULO|scale|scale|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULO|NULO|NULO|NULO|NULO|NULO|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULO|NULO|NULO|NULO|NULO|NULO|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|0|0|0|3|0|0|  
|MAXIMUM_SCALE|0|7|0|3|7|7|  
|SQL_DATA_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TYPE_TIMESTAMPOFFSET|  
|SQL_DATETIME_SUB|SQL_CODE_DATE|NULO|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULO|  
|NUM_PREC_RADIX|NULO|NULO|NULO|NULO|NULO|NULO|  
|INTERVAL_PRECISION|NULO|NULO|NULO|NULO|NULO|NULO|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="see-also"></a>Consulte Também  
 [Metadados &#40;&#41;ODBC](../../database-engine/dev-guide/metadata-odbc.md)  
  
  
