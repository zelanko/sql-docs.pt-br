---
title: Mapeamento SQLSetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5284fd0065e3d1b2c23725a05b71dbb5d2f0810b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792997"
---
# <a name="sqlsetstmtoption-mapping"></a>Mapeamento SQLSetStmtOption
Quando um aplicativo chama **SQLSetStmtOption** por meio de ODBC *3.x* driver, a chamada para  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 resulta da seguinte maneira:  
  
-   Se *fOption* indica um atributo de instrução definidas pelo ODBC é uma cadeia de caracteres, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica um atributo de instrução definidas pelo ODBC que retorna um valor inteiro de 32 bits, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica um atributo de instrução definidos pelo driver, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o **StatementHandle** argumento é definido como o valor na *hstmt*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o valor de *vParam*.  
  
 Porque o Gerenciador de Driver não sabe se o atributo de instrução definidos pelo driver precisa de uma cadeia de caracteres ou um valor de inteiro de 32 bits, ele deve passar um valor válido para o *StringLength* argumento de **SQLSetStmtAttr**. Se o driver definiu semântica especial para atributos de instrução definidos pelo driver e precisa ser chamado usando **SQLSetStmtOption**, ele deve suportar **SQLSetStmtOption**.  
  
 Se um aplicativo chamar **SQLSetStmtOption** para definir uma opção de instrução específica do driver no ODBC *3.x* driver e a opção foi definida em um ODBC *2.x* versão das driver, uma nova constante de manifesto deve ser definida para a opção no ODBC *3.x* driver. Se a constante de manifesto antiga é usada na chamada para **SQLSetStmtOption**, o Gerenciador de Driver chamará **SQLSetStmtAttr** com o *StringLength* argumento definido como 0.  
  
 Quando um aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS como SQL_UB_ON no ODBC *3.x* driver, o atributo da instrução SQL_ATTR_USE_BOOKMARKS está definido como SQL_UB_FIXED. SQL_UB_ON é a mesma constante como SQL_UB_FIXED. O Gerenciador de Driver passa SQL_UB_FIXED por meio do driver. SQL_UB_FIXED foi preterido no ODBC *3.x*, mas um ODBC *3.x* driver deve implementá-lo para trabalhar com ODBC *2.x* aplicativos que usam indicadores de comprimento fixo.  
  
 Para um ODBC *3.x* driver, o Gerenciador de Driver não verifica se *opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START.
