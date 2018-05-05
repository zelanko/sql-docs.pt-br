---
title: Mapeamento de SQLGetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02eaacbe3503b5d93677633aa0e98326b14e304f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetstmtoption-mapping"></a>Mapeamento de SQLGetStmtOption
Quando um aplicativo chama **SQLGetStmtOption** para um ODBC 3 *. x* driver que não dá suporte a ele, a chamada para  
  
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
  
 Nos três casos anteriores, o *StatementHandle* argumento é definido como o valor em *hstmt*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o mesmo valor como *pvParam*.  
  
 Para obter opções de conexão de cadeia de caracteres definidas pelo ODBC, o Gerenciador de Driver define o *BufferLength* argumentos na chamada para **SQLGetConnectAttr** para o tamanho máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão não-String, *BufferLength* é definido como 0.  
  
 A opção de instrução SQL_GET_BOOKMARK foi preterida no ODBC 3 *. x*. Para um ODBC 3 *. x* driver para trabalhar com ODBC 2. *x* aplicativos que usam SQL_GET_BOOKMARK, deverá dar suporte a SQL_GET_BOOKMARK. Para um ODBC 3 *. x* driver para trabalhar com ODBC 2. *x* aplicativos, deverá dar suporte a configuração SQL_USE_BOOKMARKS para SQL_UB_ON e deve expor indicadores de comprimento fixo. Se um ODBC 3 *. x* driver dá suporte a indicadores de comprimento variável apenas, indicadores de não-comprimento fixo, ele deve retornar SQLSTATE HYC00 (recurso opcional não implementado) se um ODBC 2. *x* aplicativo tenta configurar SQL_USE_BOOKMARKS SQL_UB_ON.  
  
 Para um ODBC 3 *. x* driver, o Gerenciador de Driver não verifica para ver se *opção* é entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX ou é maior do que SQL_CONNECT_OPT_DRVR_START. O driver deve verificar isso.
