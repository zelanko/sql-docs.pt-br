---
title: Conformidade de Campo do Descritor | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305927"
---
# <a name="descriptor-field-conformance"></a>Conformidade de campo de descritor
A tabela a seguir indica o nível de conformidade de cada campo de cabeçalho descritor ODBC, onde isso está bem definido.  
  
|Função|Compatibilidade com nível|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Núcleo|  
|SQL_DESC_ARRAY_SIZE|Núcleo|  
|SQL_DESC_ARRAY_STATUS_PTR|Núcleo (para APD, IPR e IRD); Nível 1 (para ARD)|  
|SQL_DESC_BIND_OFFSET_PTR|Núcleo|  
|SQL_DESC_BIND_TYPE|Núcleo|  
|SQL_DESC_COUNT|Núcleo|  
|SQL_DESC_ROWS_PROCESSED_PTR|Núcleo|  
  
 A tabela a seguir indica o nível de conformidade de cada campo de registro de descritor ODBC, onde isso está bem definido.  
  
|Função|Compatibilidade com nível|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nível 2|  
|SQL_DESC_BASE_COLUMN_NAME|Núcleo|  
|SQL_DESC_BASE_TABLE_NAME|Nível 1|  
|SQL_DESC_CASE_SENSITIVE|Núcleo|  
|SQL_DESC_CATALOG_NAME|Nível 2|  
|SQL_DESC_CONCISE_TYPE|Núcleo|  
|SQL_DESC_DATA_PTR|Núcleo|  
|CÓDIGO SQL_DESC_DATETIME_INTERVAL_|Núcleo[1]|  
|precisão SQL_DESC_DATETIME_INTERVAL_|Núcleo[1]|  
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
|SQL_DESC_PARAMETER_TYPE|Núcleo/Nível 2[2]|  
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
  
 [1] O suporte para esses campos de registro é necessário somente se o driver suportar os tipos de dados aplicáveis.  
  
 [2] Para conformidade de nível de núcleo, o driver deve suportar SQL_PARAM_INPUT. Para conformidade de interface nível 2, o driver também deve suportar SQL_PARAM_INPUT_OUTPUT e SQL_PARAM_OUTPUT.
