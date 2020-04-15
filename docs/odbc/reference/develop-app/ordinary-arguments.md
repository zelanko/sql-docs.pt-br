---
title: Argumentos Ordinários | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97362f93e91ccd8b592b4c05a0714b7602c1ba94
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282456"
---
# <a name="ordinary-arguments"></a>Argumentos comuns
Quando um argumento de seqüência de função de catálogo é um argumento comum, ele é tratado como uma seqüência literal. Um argumento comum não aceita nem um padrão de pesquisa de strings nem uma lista de valores. O caso de um argumento comum é significativo, e os caracteres de citação na seqüência são levados literalmente. Esses argumentos são tratados como argumentos comuns se o atributo de declaração SQL_ATTR_METADATA_ID for definido para SQL_FALSE; eles são tratados como argumentos identificadores, em vez disso, se este atributo for definido como SQL_TRUE.  
  
 Se um argumento ordinário for definido como um ponteiro nulo e o argumento for um argumento necessário, a função retorna SQL_ERROR e SQLSTATE HY009 (uso inválido do ponteiro nulo). Se um argumento comum é definido como um ponteiro nulo e o argumento não é um argumento necessário, o comportamento do argumento é dependente do motorista. Os argumentos necessários estão listados na tabela a seguir.  
  
|Função|Argumentos necessários|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*Tablename*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*Tablename*|  
|**SQLSpecialColumns**|*Tablename*|  
|**SQLStatistics**|*Tablename*|
