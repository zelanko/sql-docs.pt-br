---
title: Função SQLRemoveDefaultDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90270f119b351592348287823c2b9d879a15154b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821114"
---
# <a name="sqlremovedefaultdatasource-function"></a>Função SQLRemoveDefaultDataSource
**Conformidade com**  
 Versão introduzida: ODBC 1.0, preterido  
  
 **Resumo**  
 No ODBC 3.0, o **SQLRemoveDefaultDataSource** foi substituída por uma chamada à função [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) com um *frequentes* argumento de ODBC_REMOVE_DEFAULT_DSN. Se um ODBC 2 *. x* programa de instalação chama esta função, o instalador ODBC mapeá-lo para o seguinte **SQLConfigDataSource** chamar:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
