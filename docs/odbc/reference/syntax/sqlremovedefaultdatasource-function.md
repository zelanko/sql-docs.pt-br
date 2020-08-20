---
description: Função SQLRemoveDefaultDataSource
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0010e59cc4dfad2d54b8b1c4e59e83ea72fcd3ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487084"
---
# <a name="sqlremovedefaultdatasource-function"></a>Função SQLRemoveDefaultDataSource
**Conformidade**  
 Versão introduzida: ODBC 1,0, preterido  
  
 **Resumo**  
 No ODBC 3,0, a função **SQLRemoveDefaultDataSource** foi substituída por uma chamada para [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) com um argumento *fRequest* de ODBC_REMOVE_DEFAULT_DSN. Se um programa de instalação ODBC 2 *. x* chamar essa função, o instalador ODBC o mapeará para a seguinte chamada **SQLConfigDataSource** :  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
