---
title: SQLFreeEnv Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c1ab12a975d7b9c0aba77db9af31accac398a16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199409"
---
# <a name="sqlfreeenv-mapping"></a>Mapeamento SQLFreeEnv
Quando um aplicativo chama **SQLFreeEnv** por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLFreeEnv(henv)   
```  
  
 é mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 com o *manipular* argumento definido como o valor na *henv*.
