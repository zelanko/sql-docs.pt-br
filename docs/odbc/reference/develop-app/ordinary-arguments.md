---
title: Argumentos comuns | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a97c5c7125b24239d0eaae1a75efdd65c37d7b04
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ordinary-arguments"></a>Argumentos comuns
Quando um argumento de cadeia de caracteres de função de catálogo é um argumento normal, ele é tratado como uma cadeia de caracteres literal. Um argumento comum aceita um padrão de pesquisa de cadeia de caracteres, nem uma lista de valores. No caso de um argumento comum é significativo e caracteres de aspas na cadeia de caracteres exibidos literalmente. Esses argumentos são tratados como argumentos comuns se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_FALSE; eles são tratados como argumentos de identificador em vez disso, se esse atributo é definido como SQL_TRUE.  
  
 Se um argumento comum é definido como um ponteiro nulo e o argumento é um argumento necessário, a função retornará SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro nulo). Se um argumento comum é definido como um ponteiro nulo e o argumento não é um argumento necessário, o comportamento do argumento é dependente do driver. Os argumentos necessários são listados na tabela a seguir.  
  
|Função|Argumentos necessários|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
