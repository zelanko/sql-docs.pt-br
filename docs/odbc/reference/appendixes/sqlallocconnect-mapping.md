---
title: Mapeamento de SQLAllocConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65c23f41ea9176c460c8fb32ece5e74dfb803541
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065020"
---
# <a name="sqlallocconnect-mapping"></a>Mapeamento SQLAllocConnect
Quando um aplicativo chama **SQLAllocConnect** por meio de um ODBC 3. *x* Driver, a chamada para **SQLAllocConnect**(*HENV*, *phdbc*) é mapeada para **SQLAllocHandle** da seguinte maneira:  
  
1.  O Gerenciador de driver aloca uma conexão e a retorna para o aplicativo.  
  
2.  Quando o aplicativo estabelece uma conexão, o Gerenciador de driver chama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     no driver com *InputHandle* definido como *HENV*e *OutputHandlePtr* definido como *phdbc*.
