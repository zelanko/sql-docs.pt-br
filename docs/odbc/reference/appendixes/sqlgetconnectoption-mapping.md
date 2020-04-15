---
title: Mapeamento de opções sqlgetconnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d2905bd6793d032e485183c8f553cef2cdefda3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301997"
---
# <a name="sqlgetconnectoption-mapping"></a>Mapeamento SQLGetConnectOption
Quando um aplicativo chama **SQLGetConnectOption** através de um driver ODBC *3.x,* a chamada para  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 é mapeado da seguinte forma:  
  
-   Se *fOption* indicar uma opção de conexão definida pelo ODBC que retorna uma string, o Gerenciador de drivers chamará  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de conexão definida pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver seleção chama  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de declaração definida pelo driver, o Gerenciador de driver saqueie  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nos três casos anteriores, o argumento *ConnectionHandle* é definido como o valor em *hdbc*, o argumento *Atributo* é definido como o valor em *fOption*, e o argumento *ValuePtr* é definido para o mesmo valor que *pvParam*.  
  
 Para opções de conexão de seqüência definidas pelo ODBC, o Gerenciador de driver define o argumento *BufferLength* na chamada para **SQLGetConnectAttr** para o comprimento máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão sem cadeia, *BufferLength* é definido como 0.  
  
 Para um driver ODBC *3.x,* o Driver Manager não verifica mais se *a Opção* está entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX, ou se é maior do que SQL_CONNECT_OPT_DRVR_START. O motorista deve verificar a validade dos valores da opção.
