---
title: Mapeamento de SQLAllocConnect | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0188c47d6abfd294dc1a9c20c04ea7d271443a18
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocconnect-mapping"></a>Mapeamento de SQLAllocConnect
Quando um aplicativo chama **SQLAllocConnect** por meio de um ODBC 3.* x* driver, a chamada para **SQLAllocConnect**(*henv*, *phdbc*) é mapeado para **SQLAllocHandle** da seguinte maneira:  
  
1.  O Gerenciador de Driver aloca uma conexão e retorna-a para o aplicativo.  
  
2.  Quando o aplicativo estabelece uma conexão, chama o Gerenciador de Driver  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     no driver com *InputHandle* definida como *henv*, e *OutputHandlePtr* definida como *phdbc*.

