---
title: Mapeamento SQLAllocConnect | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25e72cd3830cea8504983f4348f6c200261490f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305517"
---
# <a name="sqlallocconnect-mapping"></a>Mapeamento SQLAllocConnect
Quando um aplicativo chama **SQLAllocConnect** através de um ODBC 3. *x* driver, a chamada para **SQLAllocConnect***(henv*, *phdbc)* é mapeada para **SQLAllocHandle** da seguinte forma:  
  
1.  O Gerenciador de Driver aloca uma conexão e a devolve ao aplicativo.  
  
2.  Quando o aplicativo estabelece uma conexão, o Driver Manager chama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     no driver com *InputHandle* definido como *henv*, e *OutputHandlePtr* definido como *phdbc*.
