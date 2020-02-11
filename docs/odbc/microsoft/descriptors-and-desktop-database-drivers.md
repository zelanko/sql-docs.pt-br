---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0096dad8fbb4cf9847385759702e39ac074c4c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68112056"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descritores e drivers de banco de dados de área de trabalho
Um descritor é uma estrutura de dados que contém informações sobre os dados da coluna ou os parâmetros dinâmicos. **SQLGetDescField** pode ser usado para recuperar os descritores com suporte listados abaixo. Os descritores de parâmetro de implementação (IPD) não são populados automaticamente porque não há suporte para **SQLDescribeParam** . Os campos de descritores que não estão disponíveis por meio do Jet (como SQL_DESC_BASE_TABLE_NAME) também não têm suporte.  
  
 Para obter mais informações sobre os campos de descritor com suporte do Jet, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*.  
  
 Para obter mais informações sobre descritores, consulte os tópicos em "descritores" na *referência do programador de ODBC*.  
  
|Campos de descritor|Nível de suporte|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Suportado|  
|SQL_DESC_ARRAY_SIZE|Com suporte apenas para ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Suportado|  
|SQL_DESC_BIND_OFFSET_PTR|Suportado|  
|SQL_DESC_BIND_TYPE|Suportado|  
|SQL_DESC_COUNT|Suportado|  
|SQL_DESC_ROWS_PROCESSED_PTR|Com suporte apenas para ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Suportado|  
|SQL_DESC_BASE_COLUMN_NAME|Com suporte (novo)|  
|SQL_DESC_BASE_TABLE_NAME|Com suporte (novo)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSE|  
|SQL_DESC_CATALOG_NAME|Sem suporte|  
|SQL_DESC_CONCISE_TYPE|Suportado|  
|SQL_DESC_DATA_PTR|Suportado|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Suportado|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Com suporte para tipos de intervalo C|  
|SQL_DESC_DISPLAY_SIZE|Suportado|  
|SQL_DESC_FIXED_PREC_SCALE|Com suporte (verdadeiro para o Money)|  
|SQL_DESC_INDICATOR_PTR|Suportado|  
|SQL_DESC_LABEL|Suportado|  
|SQL_DESC_LENGTH|Suportado|  
|SQL_DESC_LITERAL_PREFIX|Suportado|  
|SQL_DESC_LITERAL_SUFFIX|Suportado|  
|SQL_DESC_LOCAL_TYPE_NAME|Sem suporte (retorna uma cadeia de caracteres vazia)|  
|SQL_DESC_NAME|Suportado|  
|SQL_DESC_NULLABLE|Suportado<br /><br /> **Observação** Sem suporte em versões anteriores ao Jet 4,0|  
|SQL_DESC_NUM_PREC_RADIX|Suportado|  
|SQL_DESC_OCTET_LENGTH|Suportado|  
|SQL_DESC_OCTET_LENGTH_PTR|Suportado|  
|SQL_DESC_PARAMETER_TYPE|Somente parâmetros de entrada|  
|SQL_DESC_PRECISION|Suportado|  
|SQL_DESC_SCALE|Suportado|  
|SQL_DESC_SCHEMA_NAME|Sem suporte|  
|SQL_DESC_SEARCHABLE|Suportado|  
|SQL_DESC_TABLE_NAME|Sem suporte|  
|SQL_DESC_TYPE|Suportado|  
|SQL_DESC_TYPE_NAME|Suportado|  
|SQL_DESC_UNNAMED|Suportado|  
|SQL_DESC_UNSIGNED|Suportado|  
|SQL_DESC_UPDATABLE|Suportado|
