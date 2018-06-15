---
title: Mapeamento de SQLAllocStmt | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a09c8b93369bcdcddcead96b33438dcae16f3c4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909211"
---
# <a name="sqlallocstmt-mapping"></a>Mapeamento de SQLAllocStmt
Quando um aplicativo chama **SQLAllocStmt** por meio de um ODBC 3 *. x* driver, a chamada para:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 é mapeada para **SQLAllocHandle** pelo Gerenciador de Driver no driver da seguinte maneira:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 com *InputHandle* definida como *hdbc* e *OutputHandlePtr* definida como *phstmt*.
