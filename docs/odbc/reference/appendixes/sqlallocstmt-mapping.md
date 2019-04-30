---
title: SQLAllocStmt Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 330c245d8b5839fd8a721a7399a22edea78a2417
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269945"
---
# <a name="sqlallocstmt-mapping"></a>Mapeamento SQLAllocStmt
Quando um aplicativo chama **SQLAllocStmt** por meio de um ODBC 3 *. x* driver, a chamada para:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 é mapeado para **SQLAllocHandle** pelo Gerenciador de Driver no driver da seguinte maneira:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 com o *InputHandle* definido como *hdbc* e *OutputHandlePtr* definido como *phstmt*.
