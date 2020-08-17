---
description: Usar identificadores de tipo de dados
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
ms.openlocfilehash: 54fe7267ea70dc50b0b40f16b27a1306fea533f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386272"
---
# <a name="using-data-type-identifiers"></a>Usar identificadores de tipo de dados
Os aplicativos usam identificadores de tipo de dados de duas maneiras: para descrever seus buffers para o driver e para recuperar metadados sobre o conjunto de resultados do driver para que eles possam determinar que tipo de buffers C usar para armazenar os dados. Os aplicativos chamam as seguintes funções para executar estas tarefas:  
  
-   **SQLBindParameter**, **SQLBindCol**e **SQLGetData** -para descrever o tipo de dados C de buffers de aplicativo.  
  
-   **SQLBindParameter** -para descrever o tipo de dados do SQL de parâmetros dinâmicos.  
  
-   **SQLColAttribute** e **SQLDescribeCol** -para recuperar os tipos de dados SQL das colunas do conjunto de resultados.  
  
-   **SQLDescribeParameter** -para recuperar os tipos de dados SQL de parâmetros.  
  
-   **SQLColumns**, **SQLProcedureColumns**e **SQLSpecialColumns** -para recuperar os tipos de dados SQL de várias informações de esquema  
  
-   **SQLGetTypeInfo** – para recuperar uma lista de tipos de dados com suporte  
  
 Os identificadores de tipo de dados são armazenados no campo SQL_DESC_CONCISE_TYPE de um descritor. As funções de descritor **SQLSetDescField** e **SQLSetDescRec** podem ser usadas com os tipos apropriados para executar as tarefas listadas na lista anterior. Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
