---
description: Mapeamento SQLAllocStmt
title: Mapeamento de SQLAllocStmt | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8307dce9e95c98ff92912517d5b574883d6298c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424918"
---
# <a name="sqlallocstmt-mapping"></a>Mapeamento SQLAllocStmt
Quando um aplicativo chama **SQLAllocStmt** por meio de um driver ODBC *3. x* , a chamada para:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 é mapeado para **SQLAllocHandle** pelo Gerenciador de driver no driver da seguinte maneira:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 com *InputHandle* definido como *HDBC* e *OutputHandlePtr* definido como *phstmt*.
