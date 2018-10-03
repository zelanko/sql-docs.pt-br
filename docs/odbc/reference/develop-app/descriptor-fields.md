---
title: Campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b512ff83d0002ef4a7c79b48cd8829fc2dbb9ba3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696575"
---
# <a name="descriptor-fields"></a>Campos de descritor
Os descritores de contêm *cabeçalho* e *registro* campos que descrevem completamente a colunas ou parâmetros.  
  
 Um descritor contém uma única cópia dos campos de cabeçalho a seguir. Alterar um campo de cabeçalho afeta todas as colunas ou parâmetros.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Um descritor contém zero ou mais registros de descritor. Cada registro descreve uma coluna ou parâmetro, dependendo do tipo de descritor. Quando uma nova coluna ou parâmetro está associado, um novo registro é adicionado ao descritor de. Quando uma coluna ou parâmetro é desvinculado, um registro é removido do descritor. Cada registro contém uma única cópia dos seguintes campos:  
  
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
  
 Muitos atributos de instrução correspondem ao campo de cabeçalho de um descritor. Definir esses atributos por meio de uma chamada para **SQLSetStmtAttr** e definindo o campo de cabeçalho do descritor correspondente chamando **SQLSetDescField** têm o mesmo efeito. O mesmo é verdadeiro para **SQLGetStmtAttr** e **SQLGetDescField**, ambos os quais recuperam as mesmas informações. Chamar as funções de instrução em vez das funções de descritor tem a vantagem de um identificador do descritor não precisa ser recuperado.  
  
 Os campos de cabeçalho a seguir podem ser definidos, definindo atributos de instrução:  
  
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
