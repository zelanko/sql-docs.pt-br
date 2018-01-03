---
title: Campos de descritor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed9b26cf9af0bd6b0a0a81faad62e446f01f03fd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="descriptor-fields"></a>Campos de descritor
Os descritores de contêm *cabeçalho* e *registro* campos que descrevem completamente colunas ou parâmetros.  
  
 Um descritor contém uma única cópia dos seguintes campos de cabeçalho. A alteração de um campo de cabeçalho afeta todas as colunas ou parâmetros.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Um descritor contém zero ou mais registros de descritor. Cada registro descreve uma coluna ou parâmetro, dependendo do tipo de descritor. Quando uma nova coluna ou parâmetro está associado, um novo registro é adicionado para o descritor. Quando uma coluna ou parâmetro é desvinculado, um registro é removido do descritor. Cada registro contém uma única cópia dos seguintes campos:  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 Muitos atributos de instrução correspondem ao campo de cabeçalho de um descritor. Definir esses atributos por meio de uma chamada para **SQLSetStmtAttr** e definir o campo de cabeçalho do descritor correspondente chamando **SQLSetDescField** têm o mesmo efeito. O mesmo é verdadeiro para **SQLGetStmtAttr** e **SQLGetDescField**, ambos os quais recuperam as mesmas informações. Chamar as funções de instrução, em vez de funções de descritor tem a vantagem de que um identificador do descritor não precisa ser recuperado.  
  
 Os seguintes campos de cabeçalho podem ser configurados definindo atributos de instrução:  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Contagem de registros](../../../odbc/reference/develop-app/record-count.md)  
  
-   [Registros de descritor associados](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [Campos adiados](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [Verificação de consistência](../../../odbc/reference/develop-app/consistency-check.md)
