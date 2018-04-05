---
title: Função SQLRemoveDefaultDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cba3b817fe4ec42ccf50682e504abe0783fd74ce
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovedefaultdatasource-function"></a>Função SQLRemoveDefaultDataSource
**Conformidade**  
 Versão introduzidas: ODBC 1.0, preterido  
  
 **Resumo**  
 No ODBC 3.0, o **SQLRemoveDefaultDataSource** função foi substituída por uma chamada para [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) com um *frequentes* argumento de ODBC_REMOVE_DEFAULT_DSN. Se um ODBC 2*. x* programa de instalação chama esta função, o instalador ODBC será mapeado para o seguinte **SQLConfigDataSource** chamar:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
