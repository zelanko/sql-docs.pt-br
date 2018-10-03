---
title: Conformidade de campo de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 193bdadaf36e975b1f79327bfef161daaaed427b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642304"
---
# <a name="descriptor-field-conformance"></a>Conformidade de campo de descritor
A tabela a seguir indica o nível de conformidade de cada campo de cabeçalho do descritor ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Núcleo|  
|SQL_DESC_ARRAY_SIZE|Núcleo|  
|SQL_DESC_ARRAY_STATUS_PTR|Núcleo (para APD, IPR e IRD); Nível 1 (para descartar)|  
|SQL_DESC_BIND_OFFSET_PTR|Núcleo|  
|SQL_DESC_BIND_TYPE|Núcleo|  
|SQL_DESC_COUNT|Núcleo|  
|SQL_DESC_ROWS_PROCESSED_PTR|Núcleo|  
  
 A tabela a seguir indica o nível de conformidade de cada campo de registro de descritor ODBC, que isso é bem definido.  
  
|Função|nível de conformidade|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nível 2|  
|SQL_DESC_BASE_COLUMN_NAME|Núcleo|  
|SQL_DESC_BASE_TABLE_NAME|Nível 1|  
|SQL_DESC_CASE_SENSITIVE|Núcleo|  
|SQL_DESC_CATALOG_NAME|Nível 2|  
|SQL_DESC_CONCISE_TYPE|Núcleo|  
|SQL_DESC_DATA_PTR|Núcleo|  
|CÓDIGO DE SQL_DESC_DATETIME_INTERVAL_|Core [1]|  
|PRECISÃO SQL_DESC_DATETIME_INTERVAL_|Core [1]|  
|SQL_DESC_DISPLAY_SIZE|Núcleo|  
|SQL_DESC_FIXED_PREC_SCALE|Núcleo|  
|SQL_DESC_INDICATOR_PTR|Núcleo|  
|SQL_DESC_LABEL|Nível 2|  
|SQL_DESC_LENGTH|Núcleo|  
|SQL_DESC_LITERAL_PREFIX|Núcleo|  
|SQL_DESC_LITERAL_SUFFIX|Núcleo|  
|SQL_DESC_LOCAL_TYPE_NAME|Núcleo|  
|SQL_DESC_NAME|Núcleo|  
|SQL_DESC_NULLABLE|Núcleo|  
|SQL_DESC_OCTET_LENGTH|Núcleo|  
|SQL_DESC_OCTET_LENGTH_PTR|Núcleo|  
|SQL_DESC_PARAMETER_TYPE|Nível/Core 2 [2]|  
|SQL_DESC_PRECISION|Núcleo|  
|SQL_DESC_ROWVER|Nível 1|  
|SQL_DESC_SCALE|Núcleo|  
|SQL_DESC_SCHEMA_NAME|Nível 1|  
|SQL_DESC_SEARCHABLE|Núcleo|  
|SQL_DESC_TABLE_NAME|Nível 1|  
|SQL_DESC_TYPE|Núcleo|  
|SQL_DESC_TYPE_NAME|Núcleo|  
|SQL_DESC_UNNAMED|Núcleo|  
|SQL_DESC_UNSIGNED|Núcleo|  
|SQL_DESC_UPDATABLE|Núcleo|  
  
 [1] suporte para esses campos de registro é necessário somente se o driver oferece suporte a tipos de dados aplicável.  
  
 [2] para conformidade de nível de núcleo, o driver deve oferecer suporte a SQL_PARAM_INPUT. Para conformidade de interface de nível 2, também deve oferecer suporte o driver SQL_PARAM_INPUT_OUTPUT e SQL_PARAM_OUTPUT.
