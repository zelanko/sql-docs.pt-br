---
title: Conformidade do campo do descritor | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce33adfdbfceef56936b22c549b6762521b4798
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305927"
---
# <a name="descriptor-field-conformance"></a>Conformidade de campo de descritor
A tabela a seguir indica o nível de conformidade de cada campo de cabeçalho de descritor ODBC, em que isso é bem definido.  
  
|Função|Compatibilidade com nível|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Núcleo|  
|SQL_DESC_ARRAY_SIZE|Núcleo|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (para APD, IPR e IRD); Nível 1 (para ARD)|  
|SQL_DESC_BIND_OFFSET_PTR|Núcleo|  
|SQL_DESC_BIND_TYPE|Núcleo|  
|SQL_DESC_COUNT|Núcleo|  
|SQL_DESC_ROWS_PROCESSED_PTR|Núcleo|  
  
 A tabela a seguir indica o nível de conformidade de cada campo de registro de descritor ODBC, em que isso é bem definido.  
  
|Função|Compatibilidade com nível|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nível 2|  
|SQL_DESC_BASE_COLUMN_NAME|Núcleo|  
|SQL_DESC_BASE_TABLE_NAME|Nível 1|  
|SQL_DESC_CASE_SENSITIVE|Núcleo|  
|SQL_DESC_CATALOG_NAME|Nível 2|  
|SQL_DESC_CONCISE_TYPE|Núcleo|  
|SQL_DESC_DATA_PTR|Núcleo|  
|CÓDIGO DE SQL_DESC_DATETIME_INTERVAL_|Núcleo [1]|  
|PRECISÃO DE SQL_DESC_DATETIME_INTERVAL_|Núcleo [1]|  
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
|SQL_DESC_PARAMETER_TYPE|Núcleo/nível 2 [2]|  
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
  
 [1] o suporte para esses campos de registro será necessário somente se o driver der suporte aos tipos de dados aplicáveis.  
  
 [2] para conformidade de nível de núcleo, o driver deve dar suporte a SQL_PARAM_INPUT. Para conformidade com a interface de nível 2, o driver também deve dar suporte a SQL_PARAM_INPUT_OUTPUT e SQL_PARAM_OUTPUT.
