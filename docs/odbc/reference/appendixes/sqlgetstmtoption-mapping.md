---
title: Mapeamento de opções sqlgetstmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300596"
---
# <a name="sqlgetstmtoption-mapping"></a>Mapeamento SQLGetStmtOption
Quando um aplicativo chama **SQLGetStmtOption** para um driver ODBC *3.x* que não o suporta, a chamada para  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 resultará da seguinte forma:  
  
-   Se *fOption* indicar uma opção de declaração definida pelo ODBC que retorna uma string, o Gerenciador de drivers chamará  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de declaração definida pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver seleção chama  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de declaração definida pelo driver, o Gerenciador de driver saqueie  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nos três casos anteriores, o argumento *StatementHandle* é definido como o valor em *hstmt*, o argumento *Atributo* é definido para o valor em *fOption*, e o argumento *ValuePtr* é definido para o mesmo valor que *pvParam*.  
  
 Para opções de conexão de seqüência definidas pelo ODBC, o Gerenciador de driver define o argumento *BufferLength* na chamada para **SQLGetConnectAttr** para o comprimento máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão sem cadeia, *BufferLength* é definido como 0.  
  
 A opção de declaração SQL_GET_BOOKMARK foi preterida em ODBC *3.x*. Para que um driver ODBC *3.x* funcione com aplicativos ODBC *2.x* que usam SQL_GET_BOOKMARK, ele deve suportar SQL_GET_BOOKMARK. Para que um driver ODBC *3.x* funcione com aplicativos ODBC *2.x,* ele deve suportar a configuração SQL_USE_BOOKMARKS a SQL_UB_ON e deve expor marcadores de comprimento fixo. Se um driver ODBC *3.x* suportar apenas marcadores de comprimento variável, não marcadores de comprimento fixo, ele deve retornar SQLSTATE HYC00 (recurso opcional não implementado) se um aplicativo ODBC *2.x* tentar definir SQL_USE_BOOKMARKS para SQL_UB_ON.  
  
 Para um driver ODBC *3.x,* o Driver Manager não verifica mais se a *Opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX, ou se é maior do que SQL_CONNECT_OPT_DRVR_START. O motorista deve verificar isso.
