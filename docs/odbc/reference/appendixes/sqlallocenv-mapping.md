---
title: Mapeamento de SQLAllocEnv | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb26e3443fabda2d6490c071b1f2668895e66b8d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304037"
---
# <a name="sqlallocenv-mapping"></a>Mapeamento SQLAllocEnv
Quando um aplicativo chama **SQLAllocEnv** por meio de um driver ODBC *3. x* , a chamada para **SQLAllocEnv**(*phenv*) é mapeada para **SQLAllocHandle** da seguinte maneira:  
  
1.  O Gerenciador de driver aloca um identificador de ambiente e o retorna para o aplicativo. O Gerenciador de driver chama **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC2.  
  
2.  Quando o aplicativo estabelece a primeira conexão com um driver, o Gerenciador de driver chama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     no driver com *OutputHandlePtr* definido como *phenv*.
