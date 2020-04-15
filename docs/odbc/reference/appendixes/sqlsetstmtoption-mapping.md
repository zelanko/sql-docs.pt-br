---
title: Mapeamento de opções sqlsetstmt | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91264cee0dfceeb7195e2bad40d1638a88e1e01a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304897"
---
# <a name="sqlsetstmtoption-mapping"></a>Mapeamento SQLSetStmtOption
Quando um aplicativo chama **SQLSetStmtOption** através de um driver ODBC *3.x,* a chamada para  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 resultará da seguinte forma:  
  
-   Se *fOption* indicar um atributo de declaração definido pelo ODBC que é uma string, o Gerenciador de driver saqueia  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indicar um atributo de declaração definido pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver seleção chama  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indicar um atributo de declaração definido pelo driver, o Gerenciador de driver saqueie  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o argumento **StatementHandle** é definido como valor em *hstmt*, o argumento *Atributo* é definido como valor em *fOption*, e o argumento *ValuePtr* é definido para o valor como *vParam*.  
  
 Como o Driver Manager não sabe se o atributo de declaração definido pelo driver precisa de um valor inteiro de string ou 32 bits, ele tem que passar em um valor válido para o argumento *StringLength* do **SQLSetStmtAttr**. Se o driver tiver definido a semântica especial para atributos de declaração definidos pelo driver e precisar ser chamado usando **SQLSetStmtOption,** ele deve suportar **SQLSetStmtOption**.  
  
 Se um aplicativo chamar **SQLSetStmtOption** para definir uma opção de instrução específica do driver em um driver ODBC *3.x* e a opção for definida em uma versão ODBC *2.x* do driver, uma nova constante de manifesto deve ser definida para a opção no driver ODBC *3.x.* Se a antiga constante de manifesto for usada na chamada para **SQLSetStmtOption,** o Gerenciador de driver chamará **SQLSetStmtAttr** com o argumento *StringLength* definido como 0.  
  
 Quando um aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS para SQL_UB_ON em um driver ODBC *3.x,* o atributo de declaração SQL_ATTR_USE_BOOKMARKS é definido como SQL_UB_FIXED. SQL_UB_ON é a mesma constante que SQL_UB_FIXED. O Gerente de Motorista passa SQL_UB_FIXED até o motorista. SQL_UB_FIXED foi preterido em ODBC *3.x,* mas um driver ODBC *3.x* deve implementá-lo para trabalhar com aplicativos ODBC *2.x* que usam marcadores de comprimento fixo.  
  
 Para um driver ODBC *3.x,* o Driver Manager não verifica mais se *a Opção* está entre SQL_STMT_OPT_MIN e SQL_STMT_OPT_MAX, ou se é maior do que SQL_CONNECT_OPT_DRVR_START.
