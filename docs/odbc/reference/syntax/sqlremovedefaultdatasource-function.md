---
title: "Função SQLRemoveDefaultDataSource | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed4db21dce5cf5da5234f4906116c93f9a4ea735
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlremovedefaultdatasource-function"></a>Função SQLRemoveDefaultDataSource
**Conformidade**  
 Versão introduzidas: ODBC 1.0, preterido  
  
 **Resumo**  
 No ODBC 3.0, o **SQLRemoveDefaultDataSource** função foi substituída por uma chamada para [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) com um *frequentes* argumento de ODBC_REMOVE_DEFAULT_DSN. Se um ODBC 2*. x* programa de instalação chama esta função, o instalador ODBC será mapeado para o seguinte **SQLConfigDataSource** chamar:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```

