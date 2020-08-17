---
description: Descritores e drivers de banco de dados de área de trabalho
title: Descritores e drivers de banco de dados de desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80565f912ef3136dc03cf7216ff3f997ee3eeba3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340792"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descritores e drivers de banco de dados de área de trabalho
Um descritor é uma estrutura de dados que contém informações sobre os dados da coluna ou os parâmetros dinâmicos. **SQLGetDescField** pode ser usado para recuperar os descritores com suporte listados abaixo. Os descritores de parâmetro de implementação (IPD) não são populados automaticamente porque não há suporte para **SQLDescribeParam** . Os campos de descritores que não estão disponíveis por meio do Jet (como SQL_DESC_BASE_TABLE_NAME) também não têm suporte.  
  
 Para obter mais informações sobre os campos de descritor com suporte do Jet, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.  
  
 Para obter mais informações sobre descritores, consulte os tópicos em "descritores" na *referência do programador de ODBC*.  
  
|Campos de descritor|Nível de suporte|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Com suporte|  
|SQL_DESC_ARRAY_SIZE|Com suporte apenas para ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Com suporte|  
|SQL_DESC_BIND_OFFSET_PTR|Com suporte|  
|SQL_DESC_BIND_TYPE|Com suporte|  
|SQL_DESC_COUNT|Com suporte|  
|SQL_DESC_ROWS_PROCESSED_PTR|Com suporte apenas para ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Com suporte|  
|SQL_DESC_BASE_COLUMN_NAME|Com suporte (novo)|  
|SQL_DESC_BASE_TABLE_NAME|Com suporte (novo)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSE|  
|SQL_DESC_CATALOG_NAME|Sem suporte|  
|SQL_DESC_CONCISE_TYPE|Com suporte|  
|SQL_DESC_DATA_PTR|Com suporte|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Com suporte|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Com suporte para tipos de intervalo C|  
|SQL_DESC_DISPLAY_SIZE|Com suporte|  
|SQL_DESC_FIXED_PREC_SCALE|Com suporte (verdadeiro para o Money)|  
|SQL_DESC_INDICATOR_PTR|Com suporte|  
|SQL_DESC_LABEL|Com suporte|  
|SQL_DESC_LENGTH|Com suporte|  
|SQL_DESC_LITERAL_PREFIX|Com suporte|  
|SQL_DESC_LITERAL_SUFFIX|Com suporte|  
|SQL_DESC_LOCAL_TYPE_NAME|Sem suporte (retorna uma cadeia de caracteres vazia)|  
|SQL_DESC_NAME|Com suporte|  
|SQL_DESC_NULLABLE|Com suporte<br /><br /> **Observação** Sem suporte em versões anteriores ao Jet 4,0|  
|SQL_DESC_NUM_PREC_RADIX|Com suporte|  
|SQL_DESC_OCTET_LENGTH|Com suporte|  
|SQL_DESC_OCTET_LENGTH_PTR|Com suporte|  
|SQL_DESC_PARAMETER_TYPE|Somente parâmetros de entrada|  
|SQL_DESC_PRECISION|Com suporte|  
|SQL_DESC_SCALE|Com suporte|  
|SQL_DESC_SCHEMA_NAME|Sem suporte|  
|SQL_DESC_SEARCHABLE|Com suporte|  
|SQL_DESC_TABLE_NAME|Sem suporte|  
|SQL_DESC_TYPE|Com suporte|  
|SQL_DESC_TYPE_NAME|Com suporte|  
|SQL_DESC_UNNAMED|Com suporte|  
|SQL_DESC_UNSIGNED|Com suporte|  
|SQL_DESC_UPDATABLE|Com suporte|
