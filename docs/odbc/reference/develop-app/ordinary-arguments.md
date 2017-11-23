---
title: Argumentos comuns | Microsoft Docs
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
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8cba3b5cb3f9da5963045d7fd8b015be4ed9f4cf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="ordinary-arguments"></a>Argumentos comuns
Quando um argumento de cadeia de caracteres de função de catálogo é um argumento normal, ele é tratado como uma cadeia de caracteres literal. Um argumento comum aceita um padrão de pesquisa de cadeia de caracteres, nem uma lista de valores. No caso de um argumento comum é significativo e caracteres de aspas na cadeia de caracteres exibidos literalmente. Esses argumentos são tratados como argumentos comuns se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_FALSE; eles são tratados como argumentos de identificador em vez disso, se esse atributo é definido como SQL_TRUE.  
  
 Se um argumento comum é definido como um ponteiro nulo e o argumento é um argumento necessário, a função retornará SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro nulo). Se um argumento comum é definido como um ponteiro nulo e o argumento não é um argumento necessário, o comportamento do argumento é dependente do driver. Os argumentos necessários são listados na tabela a seguir.  
  
|Função|Argumentos necessários|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*Nome de tabela*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*Nome de tabela*|  
|**SQLSpecialColumns**|*Nome de tabela*|  
|**SQLStatistics**|*Nome de tabela*|
