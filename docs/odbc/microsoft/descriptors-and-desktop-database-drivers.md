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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef79855f71d23e5a884822371f1894eb83442a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303507"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descritores e drivers de banco de dados de área de trabalho
Um descritor é uma estrutura de dados que contém informações sobre dados de coluna ou parâmetros dinâmicos. **SQLGetDescField** pode ser usado para recuperar os descritores suportados listados abaixo. Os Descritores de parâmetros de implementação (IPD) não são preenchidos automaticamente porque **o SQLDescribeParam** não é suportado. Os campos de descritores que não estão disponíveis através do Jet (como SQL_DESC_BASE_TABLE_NAME) também não são suportados.  
  
 Para obter mais informações sobre campos de descritores suportados por jato, consulte o *Guia do Programador do Motor do Banco de Dados microsoft jet*.  
  
 Para obter mais informações sobre descritores, consulte os tópicos em "Descritores" no *Programador da ODBC*.  
  
|Campos descritores|Nível de suporte|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Com suporte|  
|SQL_DESC_ARRAY_SIZE|Suportado apenas para ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Com suporte|  
|SQL_DESC_BIND_OFFSET_PTR|Com suporte|  
|SQL_DESC_BIND_TYPE|Com suporte|  
|SQL_DESC_COUNT|Com suporte|  
|SQL_DESC_ROWS_PROCESSED_PTR|Suportado apenas para ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Com suporte|  
|SQL_DESC_BASE_COLUMN_NAME|Suportado (NOVO)|  
|SQL_DESC_BASE_TABLE_NAME|Suportado (NOVO)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSO|  
|SQL_DESC_CATALOG_NAME|Sem suporte|  
|SQL_DESC_CONCISE_TYPE|Com suporte|  
|SQL_DESC_DATA_PTR|Com suporte|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Com suporte|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Suportado para tipos INTERVAL C|  
|SQL_DESC_DISPLAY_SIZE|Com suporte|  
|SQL_DESC_FIXED_PREC_SCALE|Suportado (TRUE for money)|  
|SQL_DESC_INDICATOR_PTR|Com suporte|  
|SQL_DESC_LABEL|Com suporte|  
|SQL_DESC_LENGTH|Com suporte|  
|SQL_DESC_LITERAL_PREFIX|Com suporte|  
|SQL_DESC_LITERAL_SUFFIX|Com suporte|  
|SQL_DESC_LOCAL_TYPE_NAME|Não suportado (retorna seqüência DE string EMPTY)|  
|SQL_DESC_NAME|Com suporte|  
|SQL_DESC_NULLABLE|Com suporte<br /><br /> **Nota** Sem suporte em versões anteriores ao Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Com suporte|  
|SQL_DESC_OCTET_LENGTH|Com suporte|  
|SQL_DESC_OCTET_LENGTH_PTR|Com suporte|  
|SQL_DESC_PARAMETER_TYPE|Apenas parâmetros de entrada|  
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
