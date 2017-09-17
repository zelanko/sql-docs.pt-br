---
title: Mapeamento de SQLAllocStmt | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8361f0b77e8f15f775eece7aae9b599be5e62ac
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocstmt-mapping"></a>Mapeamento de SQLAllocStmt
Quando um aplicativo chama **SQLAllocStmt** por meio de um ODBC 3*. x* driver, a chamada para:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 é mapeada para **SQLAllocHandle** pelo Gerenciador de Driver no driver da seguinte maneira:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 com *InputHandle* definida como *hdbc* e *OutputHandlePtr* definida como *phstmt*.
