---
title: Mapeamento SQLAllocEnv | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304037"
---
# <a name="sqlallocenv-mapping"></a>Mapeamento SQLAllocEnv
Quando um aplicativo chama **SQLAllocEnv** através de um driver ODBC *3.x,* a chamada para **SQLAllocEnv***(phenv)* é mapeada para **SQLAllocHandle** da seguinte forma:  
  
1.  O Gerenciador de Driver aloca uma alça de ambiente e a devolve ao aplicativo. O Driver Manager chama **o SQLSetEnvAttr** para definir o SQL_ATTR_ODBC_VERSION atributo do ambiente para SQL_OV_ODBC2.  
  
2.  Quando o aplicativo estabelece a primeira conexão a um driver, o Gerenciador de Driver chama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     no driver com *OutputHandlePtr* definido como *phenv*.
