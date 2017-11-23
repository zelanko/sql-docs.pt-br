---
title: Usando identificadores de tipo de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7dbffa887dbe29c6bf1cd686537ebd6dbe6981fa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="using-data-type-identifiers"></a>Usando identificadores de tipo de dados
Aplicativos usam identificadores de tipo de dados de duas maneiras: para descrever seus buffers para o driver e recuperar metadados sobre o conjunto de resultados de driver para que possam determinar o tipo de C armazena em buffer para usar para armazenar os dados. Aplicativos chamar as funções a seguir para executar estas tarefas:  
  
-   **SQLBindParameter**, **SQLBindCol**, e **SQLGetData** — para descrever o tipo de dados C de buffers do aplicativo.  
  
-   **SQLBindParameter** — para descrever o tipo de dados SQL de parâmetros dinâmicos.  
  
-   **SQLColAttribute** e **SQLDescribeCol** — para recuperar os tipos de dados SQL das colunas do conjunto de resultados.  
  
-   **SQLDescribeParameter** — para recuperar os tipos de dados SQL de parâmetros.  
  
-   **SQLColumns**, **SQLProcedureColumns**, e **SQLSpecialColumns** — para recuperar os tipos de dados SQL de várias informações de esquema  
  
-   **SQLGetTypeInfo** — recuperar uma lista de tipos de dados com suporte  
  
 Identificadores de tipo de dados são armazenados no campo SQL_DESC_CONCISE_TYPE de um descritor. As funções de descritor **SQLSetDescField** e **SQLSetDescRec** pode ser usado com os tipos apropriados para executar as tarefas listadas na lista anterior. Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
