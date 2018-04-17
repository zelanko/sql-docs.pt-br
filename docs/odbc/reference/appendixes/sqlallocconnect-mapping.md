---
title: Mapeamento de SQLAllocConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9271b975e1359212d1c1142ffda93f1f6c834ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlallocconnect-mapping"></a>Mapeamento de SQLAllocConnect
Quando um aplicativo chama **SQLAllocConnect** por meio de um ODBC 3. *x* driver, a chamada para **SQLAllocConnect**(*henv*, *phdbc*) é mapeado para **SQLAllocHandle** da seguinte maneira:  
  
1.  O Gerenciador de Driver aloca uma conexão e retorna-a para o aplicativo.  
  
2.  Quando o aplicativo estabelece uma conexão, chama o Gerenciador de Driver  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     no driver com *InputHandle* definida como *henv*, e *OutputHandlePtr* definida como *phdbc*.
