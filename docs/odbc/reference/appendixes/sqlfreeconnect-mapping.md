---
description: Mapeamento SQLFreeConnect
title: Mapeamento de SQLFreeConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ad5c2e5b1f519986ec59535699320aa8c11595c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461628"
---
# <a name="sqlfreeconnect-mapping"></a>Mapeamento SQLFreeConnect
Quando um aplicativo chama **SQLFreeConnect** por meio de um driver ODBC *3. x* , a chamada para  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 está mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 com o argumento *Handle* definido como o valor em *HDBC*.
