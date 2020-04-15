---
title: Usando identificadores de tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8be8eef0441d48ed03ea6ccf8f656627c1dd9b63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301407"
---
# <a name="using-data-type-identifiers"></a>Usar identificadores de tipo de dados
Os aplicativos usam identificadores de tipo de dados de duas maneiras: descrever seus buffers para o driver e recuperar metadados sobre o conjunto de resultados do driver para que eles possam determinar que tipo de buffers C usar para armazenar os dados. Os aplicativos chamam as seguintes funções para executar essas tarefas:  
  
-   **SQLBindParameter,** **SQLBindCol**e **SQLGetData** - para descrever o tipo de dados C dos buffers de aplicativos.  
  
-   **SQLBindParameter** - para descrever o tipo de dados SQL de parâmetros dinâmicos.  
  
-   **SQLColAttribute** e **SQLDescribeCol** - para recuperar os tipos de dados SQL das colunas de conjunto de resultados.  
  
-   **SQLDescribeParameter** - para recuperar os tipos de dados SQL de parâmetros.  
  
-   **Colunas SQL,** **SQLProcedureColumns**e **SQLSpecialColumns** - para recuperar os tipos de dados SQL de várias informações de esquema  
  
-   **SQLGetTypeInfo** - para recuperar uma lista de tipos de dados suportados  
  
 Os identificadores de tipo de dados são armazenados no campo SQL_DESC_CONCISE_TYPE de um descritor. As funções do descritor **SQLSetDescField** e **SQLSetDescRec** podem ser usadas com os tipos apropriados para executar as tarefas listadas na lista anterior. Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
