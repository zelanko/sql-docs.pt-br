---
title: Mapeamento de SQLGetConnectOption | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 293f6985cd81d92b8de2b264cd69216feaff00cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetconnectoption-mapping"></a>Mapeamento de SQLGetConnectOption
Quando um aplicativo chama **SQLGetConnectOption** por meio de um ODBC 3*. x* driver, a chamada para  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 é mapeado da seguinte maneira:  
  
-   Se *fOption* indica uma opção de conexão definidas pelo ODBC que retorna uma cadeia de caracteres, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indica uma opção de conexão definidas pelo ODBC que retorna um valor inteiro de 32 bits, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indica uma opção de instrução definidos pelo driver, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nos três casos anteriores, o *identificador da conexão* argumento é definido como o valor em *hdbc*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o mesmo valor como *pvParam*.  
  
 Para obter opções de conexão de cadeia de caracteres definidas pelo ODBC, o Gerenciador de Driver define o *BufferLength* argumentos na chamada para **SQLGetConnectAttr** para o tamanho máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão não-String, *BufferLength* é definido como 0.  
  
 Para um ODBC 3*. x* driver, o Gerenciador de Driver não verifica se *opção* é entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX ou é maior do que SQL_CONNECT_OPT_DRVR_START. O driver deve verificar a validade dos valores de opção.
