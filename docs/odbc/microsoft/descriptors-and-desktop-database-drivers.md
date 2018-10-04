---
title: Drivers de banco de dados de descritores e área de trabalho | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 17058af1d7f0ab1e35c2d6b31c0337daed4c9e01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817464"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descritores e drivers de banco de dados de área de trabalho
Um descritor é uma estrutura de dados que contém informações sobre os dados da coluna ou parâmetros dinâmicos. **SQLGetDescField** pode ser usado para recuperar os descritores com suporte listados abaixo. Descritores de parâmetro de implementação (IPD) não são preenchidos automaticamente porque **SQLDescribeParam** não tem suporte. Campos de descritor que não estão disponíveis por meio de Jet (como SQL_DESC_BASE_TABLE_NAME) também não têm suporte.  
  
 Para obter mais informações sobre campos de descritor Jet com suporte, consulte o *guia do programador do Microsoft Jet banco de dados Engine*.  
  
 Para obter mais informações sobre descritores, consulte os tópicos em "Descritores" no *referência do programador de ODBC*.  
  
|Campos de descritor|Nível de suporte|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Tem suporte|  
|SQL_DESC_ARRAY_SIZE|Suporte apenas para descartar|  
|SQL_DESC_ARRAY_STATUS_PTR|Tem suporte|  
|SQL_DESC_BIND_OFFSET_PTR|Tem suporte|  
|SQL_DESC_BIND_TYPE|Tem suporte|  
|SQL_DESC_COUNT|Tem suporte|  
|SQL_DESC_ROWS_PROCESSED_PTR|Suporte apenas para descartar|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Tem suporte|  
|SQL_DESC_BASE_COLUMN_NAME|Com suporte (novo)|  
|SQL_DESC_BASE_TABLE_NAME|Com suporte (novo)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSE|  
|SQL_DESC_CATALOG_NAME|Sem suporte|  
|SQL_DESC_CONCISE_TYPE|Tem suporte|  
|SQL_DESC_DATA_PTR|Tem suporte|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Tem suporte|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Suporte para tipos C de intervalo|  
|SQL_DESC_DISPLAY_SIZE|Tem suporte|  
|SQL_DESC_FIXED_PREC_SCALE|Com suporte (verdadeiro para dinheiro)|  
|SQL_DESC_INDICATOR_PTR|Tem suporte|  
|SQL_DESC_LABEL|Tem suporte|  
|SQL_DESC_LENGTH|Tem suporte|  
|SQL_DESC_LITERAL_PREFIX|Tem suporte|  
|SQL_DESC_LITERAL_SUFFIX|Tem suporte|  
|SQL_DESC_LOCAL_TYPE_NAME|Não tem suporte (retorna cadeia de caracteres vazia)|  
|SQL_DESC_NAME|Tem suporte|  
|SQL_DESC_NULLABLE|Tem suporte<br /><br /> **Observação** sem suporte em versões anteriores do Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Tem suporte|  
|SQL_DESC_OCTET_LENGTH|Tem suporte|  
|SQL_DESC_OCTET_LENGTH_PTR|Tem suporte|  
|SQL_DESC_PARAMETER_TYPE|Somente os parâmetros de entrada|  
|SQL_DESC_PRECISION|Tem suporte|  
|SQL_DESC_SCALE|Tem suporte|  
|SQL_DESC_SCHEMA_NAME|Sem suporte|  
|SQL_DESC_SEARCHABLE|Tem suporte|  
|SQL_DESC_TABLE_NAME|Sem suporte|  
|SQL_DESC_TYPE|Tem suporte|  
|SQL_DESC_TYPE_NAME|Tem suporte|  
|SQL_DESC_UNNAMED|Tem suporte|  
|SQL_DESC_UNSIGNED|Tem suporte|  
|SQL_DESC_UPDATABLE|Tem suporte|
