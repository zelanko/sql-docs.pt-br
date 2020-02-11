---
title: Mapeamento de SQLSetStmtOption | Microsoft Docs
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
ms.openlocfilehash: dc4ed430b301f2b191c0586c0a54af19a2d2d526
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091676"
---
# <a name="sqlsetstmtoption-mapping"></a>Mapeamento SQLSetStmtOption
Quando um aplicativo chama **SQLSetStmtOption** por meio de um driver ODBC *3. x* , a chamada para  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 o resultado será o seguinte:  
  
-   Se *fOption* indicar um atributo de instrução definido pelo ODBC que é uma cadeia de caracteres, o Gerenciador de driver chamará  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indicar um atributo de instrução definido pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver chamará  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indicar um atributo de instrução definido pelo driver, o Gerenciador de driver chamará  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o argumento **StatementHandle** é definido como o valor em *HSTMT*, o argumento de *atributo* é definido como o valor em *fOption*e o argumento *ValuePtr* é definido como o valor como *vParam*.  
  
 Como o Gerenciador de driver não sabe se o atributo de instrução definido pelo driver precisa de um valor inteiro de cadeia de caracteres ou de 32 bits, ele precisa passar um valor válido para o argumento *StringLength* de **SQLSetStmtAttr**. Se o driver tiver definido semântica especial para atributos de instrução definidos pelo driver e precisar ser chamado usando **SQLSetStmtOption**, ele deverá dar suporte a **SQLSetStmtOption**.  
  
 Se um aplicativo chamar **SQLSetStmtOption** para definir uma opção de instrução específica de driver em um driver ODBC *3. x* e a opção tiver sido definida em uma versão ODBC *2. x* do driver, uma nova constante de manifesto deverá ser definida para a opção no driver ODBC *3. x* . Se a constante de manifesto antiga for usada na chamada para **SQLSetStmtOption**, o Gerenciador de driver chamará **SQLSetStmtAttr** com o argumento *StringLength* definido como 0.  
  
 Quando um aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS para SQL_UB_ON em um driver ODBC *3. x* , o atributo da instrução SQL_ATTR_USE_BOOKMARKS é definido como SQL_UB_FIXED. SQL_UB_ON é a mesma constante que SQL_UB_FIXED. O Gerenciador de driver passa SQL_UB_FIXED para o driver. O SQL_UB_FIXED foi preterido no ODBC *3. x*, mas um driver ODBC *3. x* deve implementá-lo para trabalhar com aplicativos ODBC *2. x* que usam indicadores de comprimento fixo.  
  
 Para um driver ODBC *3. x* , o Gerenciador de driver não verifica mais para ver se a *opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START.
