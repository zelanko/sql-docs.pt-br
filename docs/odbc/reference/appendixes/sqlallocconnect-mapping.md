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
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09fc3b99f519df49202f8834ca16f585cae903a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlallocconnect-mapping"></a>Mapeamento de SQLAllocConnect
Quando um aplicativo chama **SQLAllocConnect** por meio de um ODBC 3. *x* driver, a chamada para **SQLAllocConnect**(*henv*, *phdbc*) é mapeado para **SQLAllocHandle** da seguinte maneira:  
  
1.  O Gerenciador de Driver aloca uma conexão e retorna-a para o aplicativo.  
  
2.  Quando o aplicativo estabelece uma conexão, chama o Gerenciador de Driver  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     no driver com *InputHandle* definida como *henv*, e *OutputHandlePtr* definida como *phdbc*.
