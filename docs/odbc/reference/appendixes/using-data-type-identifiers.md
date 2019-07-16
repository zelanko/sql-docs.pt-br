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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b5e9fea64986bf595676540d74bb87a6e62521c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070012"
---
# <a name="using-data-type-identifiers"></a>Usar identificadores de tipo de dados
Aplicativos usam identificadores de tipo de dados de duas maneiras: para descrever seus buffers para o driver e recuperar metadados sobre o conjunto de resultados de driver para que eles possam determinar que tipo de C armazena em buffer para usar para armazenar os dados. Aplicativos chamam as funções a seguir para executar essas tarefas:  
  
-   **SQLBindParameter**, **SQLBindCol**, e **SQLGetData** - para descrever o tipo de dados C de buffers do aplicativo.  
  
-   **SQLBindParameter** - para descrever o tipo de dados SQL de parâmetros dinâmicos.  
  
-   **SQLColAttribute** e **SQLDescribeCol** – para recuperar os tipos de dados SQL das colunas do conjunto de resultados.  
  
-   **SQLDescribeParameter** – para recuperar os tipos de dados SQL de parâmetros.  
  
-   **SQLColumns**, **SQLProcedureColumns**, e **SQLSpecialColumns** – para recuperar os tipos de dados SQL de várias informações de esquema  
  
-   **SQLGetTypeInfo** – para recuperar uma lista de tipos de dados com suporte  
  
 Identificadores de tipo de dados são armazenados no campo de um descritor de SQL_DESC_CONCISE_TYPE. As funções de descritor **SQLSetDescField** e **SQLSetDescRec** pode ser usado com os tipos apropriados para executar as tarefas listadas na lista anterior. Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
