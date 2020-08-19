---
description: Mapeamento SQLFreeEnv
title: Mapeamento de SQLFreeEnv | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c3ccbf3175c7f17d06b55799463fb7115997e01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421490"
---
# <a name="sqlfreeenv-mapping"></a>Mapeamento SQLFreeEnv
Quando um aplicativo chama **SQLFreeEnv** por meio de um driver ODBC *3. x* , a chamada para  
  
```  
SQLFreeEnv(henv)   
```  
  
 está mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 com o argumento *Handle* definido como o valor em *HENV*.
