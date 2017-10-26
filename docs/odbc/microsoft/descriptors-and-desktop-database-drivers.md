---
title: "Drivers de banco de dados de área de trabalho e de descritores | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 67f656acd349419d7fc3d1c264985beeb36298ce
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="descriptors-and-desktop-database-drivers"></a>Descritores e Drivers de banco de dados de área de trabalho
Um descritor é uma estrutura de dados que contém informações sobre os dados da coluna ou parâmetros dinâmicos. **SQLGetDescField** pode ser usado para recuperar os descritores com suporte listados abaixo. Descritores de parâmetro de implementação (IPD) não são preenchidos automaticamente porque **SQLDescribeParam** não tem suporte. Campos de descritor que não estão disponíveis por meio de Jet (como SQL_DESC_BASE_TABLE_NAME) também não são suportados.  
  
 Para obter mais informações sobre campos de descritor Jet com suporte, consulte o *guia do programador do Microsoft Jet Database Engine*.  
  
 Para obter mais informações sobre descritores, consulte os tópicos em "Descritores" no *referência do programador de ODBC*.  
  
|Campos de descritor|Nível de suporte|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Tem suporte|  
|SQL_DESC_ARRAY_SIZE|Há suporte apenas para descartar|  
|SQL_DESC_ARRAY_STATUS_PTR|Tem suporte|  
|SQL_DESC_BIND_OFFSET_PTR|Tem suporte|  
|SQL_DESC_BIND_TYPE|Tem suporte|  
|SQL_DESC_COUNT|Tem suporte|  
|SQL_DESC_ROWS_PROCESSED_PTR|Há suporte apenas para descartar|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Tem suporte|  
|SQL_DESC_BASE_COLUMN_NAME|Com suporte (novo)|  
|SQL_DESC_BASE_TABLE_NAME|Com suporte (novo)|  
|SQL_DESC_CASE_SENSITIVE|Sempre FALSE|  
|SQL_DESC_CATALOG_NAME|Sem suporte|  
|SQL_DESC_CONCISE_TYPE|Tem suporte|  
|SQL_DESC_DATA_PTR|Tem suporte|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Tem suporte|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Suporte para tipos de intervalo C|  
|SQL_DESC_DISPLAY_SIZE|Tem suporte|  
|SQL_DESC_FIXED_PREC_SCALE|Com suporte (TRUE dinheiro)|  
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

