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
ms.openlocfilehash: 6070d7a9d9a7d2eafa35b87c94d6cfd320f916ae
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793573"
---
# <a name="sqlfreeenv-mapping"></a>Mapeamento SQLFreeEnv
Quando um aplicativo chama **SQLFreeEnv** por meio de ODBC *3.x* driver, a chamada para  
  
```  
SQLFreeEnv(henv)   
```  
  
 é mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 com o *manipular* argumento definido como o valor na *henv*.
