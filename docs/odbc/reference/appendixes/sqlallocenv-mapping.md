---
title: SQLAllocEnv Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 841310d1e51084ae6a61c629b8782a8b84c665f8
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793578"
---
# <a name="sqlallocenv-mapping"></a>Mapeamento SQLAllocEnv
Quando um aplicativo chama **SQLAllocEnv** por meio de ODBC *3.x* driver, a chamada para **SQLAllocEnv**(*phenv*) é mapeado para **SQLAllocHandle** da seguinte maneira:  
  
1.  O Gerenciador de Driver aloca um identificador de ambiente e retorna para o aplicativo. As chamadas de Gerenciador de Driver **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC2.  
  
2.  Quando o aplicativo estabelece a primeira conexão para um driver, o Gerenciador de Driver chama  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     no driver com *OutputHandlePtr* definido como *phenv*.
