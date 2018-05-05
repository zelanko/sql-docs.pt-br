---
title: Mapeamento de SQLFreeConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d646cc5af246925d89b571734eb967ddc7195676
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreeconnect-mapping"></a>Mapeamento de SQLFreeConnect
Quando um aplicativo chama **SQLFreeConnect** por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 é mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 com o *tratar* argumento definido como o valor em *hdbc*.
