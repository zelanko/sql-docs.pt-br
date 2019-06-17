---
title: Mapeamento SQLGetStmtOption | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2423d41b1e9c549b7202a68fb2a0e085e0a6e11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297955"
---
# <a name="sqlgetstmtoption-mapping"></a>Mapeamento SQLGetStmtOption
Quando um aplicativo chama **SQLGetStmtOption** para um ODBC 3 *. x* driver que não oferece suporte a ele, a chamada para  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 resulta da seguinte maneira:  
  
-   Se *fOption* indica uma opção de instrução definidas pelo ODBC que retorna uma cadeia de caracteres, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indica uma opção de instrução definidas pelo ODBC que retorna um valor inteiro de 32 bits, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indica uma opção de instrução definidos pelo driver, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nos três casos anteriores, o *StatementHandle* argumento é definido como o valor na *hstmt*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o mesmo valor de *pvParam*.  
  
 Para obter opções de conexão de cadeia de caracteres definidas pelo ODBC, o Gerenciador de Driver define o *BufferLength* argumento na chamada para **SQLGetConnectAttr** para o tamanho máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão não cadeia de caracteres, *BufferLength* é definido como 0.  
  
 A opção de instrução SQL_GET_BOOKMARK foi preterida no ODBC 3 *. x*. Para um ODBC 3 *. x* driver para trabalhar com ODBC 2. *x* aplicativos que usam SQL_GET_BOOKMARK, ele deve oferecer suporte a SQL_GET_BOOKMARK. Para um ODBC 3 *. x* driver para trabalhar com ODBC 2. *x* aplicativos, ele deve oferecer suporte a definição de SQL_USE_BOOKMARKS como SQL_UB_ON e deve expor os indicadores de comprimento fixo. Se um ODBC 3 *. x* driver dá suporte a indicadores de comprimento variável apenas, indicadores de não-comprimento fixo, ele deve retornar o SQLSTATE HYC00 (recurso opcional não implementado) se um ODBC 2. *x* aplicativo tenta configurar SQL_USE_BOOKMARKS SQL_UB_ON.  
  
 Para um ODBC 3 *. x* driver, o Gerenciador de Driver não verifica para ver se *opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START. O driver deve verificar isso.
