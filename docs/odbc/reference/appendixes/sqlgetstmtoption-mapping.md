---
description: Mapeamento SQLGetStmtOption
title: Mapeamento de SQLGetStmtOption | Microsoft Docs
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
ms.openlocfilehash: 01d099c4802c05f8e5bd1e093987f2c3993ac9c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448976"
---
# <a name="sqlgetstmtoption-mapping"></a>Mapeamento SQLGetStmtOption
Quando um aplicativo chama **SQLGetStmtOption** para um driver ODBC *3. x* que não oferece suporte a ele, a chamada para  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 o resultado será o seguinte:  
  
-   Se *fOption* indicar uma opção de instrução definida pelo ODBC que retorna uma cadeia de caracteres, o Gerenciador de driver chamará  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de instrução definida pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver chamará  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Se *fOption* indicar uma opção de instrução definida pelo driver, o Gerenciador de driver chamará  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 Nos três casos anteriores, o argumento *StatementHandle* é definido como o valor em *HSTMT*, o argumento de *atributo* é definido como o valor em *fOption*e o argumento *ValuePtr* é definido com o mesmo valor de *pvParam*.  
  
 Para opções de conexão de cadeia de caracteres definidas pelo ODBC, o Gerenciador de driver define o argumento *BufferLength* na chamada para **SQLGetConnectAttr** com o comprimento máximo predefinido (SQL_MAX_OPTION_STRING_LENGTH); para uma opção de conexão não cadeia de caracteres, *BufferLength* é definido como 0.  
  
 A opção de instrução SQL_GET_BOOKMARK foi preterida no ODBC *3. x*. Para que um driver ODBC *3. x* funcione com aplicativos ODBC *2. x* que usam SQL_GET_BOOKMARK, ele deve dar suporte a SQL_GET_BOOKMARK. Para que um driver ODBC *3. x* funcione com aplicativos ODBC *2. x* , ele deve dar suporte à configuração SQL_USE_BOOKMARKS para SQL_UB_ON e deve expor indicadores de comprimento fixo. Se um driver ODBC *3. x* oferecer suporte apenas a indicadores de comprimento variável, não a indicadores de comprimento fixo, ele deverá retornar SQLSTATE HYC00 (recurso opcional não implementado) se um aplicativo ODBC *2. x* tentar definir SQL_USE_BOOKMARKS como SQL_UB_ON.  
  
 Para um driver ODBC *3. x* , o Gerenciador de driver não verifica mais para ver se a *opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START. O driver deve verificar isso.
