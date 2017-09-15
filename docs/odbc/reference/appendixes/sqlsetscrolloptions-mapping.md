---
title: Mapeamento de SQLSetScrollOptions | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6774f99f1a9596964a965e34f800141fd58e9fb
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-mapping"></a>Mapeamento de SQLSetScrollOptions
Quando um aplicativo chama **SQLSetScrollOptions** por meio de um ODBC 3*. x* driver e o driver não oferece suporte **SQLSetScrollOptions**, a chamada para  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 resulta da seguinte maneira:  
  
-   Uma chamada para  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     com o *informação* argumento definido como um dos valores na tabela a seguir, dependendo do valor da *KeysetSize* argumento **SQLSetScrollOptions**.  
  
    |*Argumento KeysetSize*|*Argumento de tipo de informação*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Um valor maior que o *RowsetSize* argumento|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Se o valor da *KeysetSize* argumento não estiver listado na tabela anterior, a chamada para **SQLSetScrollOptions** retorna SQLSTATE S1107 (valor fora do intervalo de linhas) e nenhuma das etapas a seguir são executada.  
  
     O Gerenciador de Driver, em seguida, verifica se o bit apropriado é definido no **InfoValuePtr* valor retornado pela chamada para **SQLGetInfo**, acordo com o valor da *desimultaneidade* argumento **SQLSetScrollOptions**.  
  
    |*Simultaneidade* argumento|*Tipo de informação* configuração|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Se o *simultaneidade* argumento não é um dos valores na tabela anterior, a chamada para **SQLSetScrollOptions** retorna SQLSTATE S1108 (opção de simultaneidade fora do intervalo) e nenhuma das etapas a seguir são executada. Se o bit apropriado (como indicado na tabela anterior) não está definido na **InfoValuePtr* para um dos valores correspondentes para o *simultaneidade* argumento, a chamada para ** SQLSetScrollOptions** retorna SQLSTATE S1C00 (o Driver não funciona), e nenhuma das etapas a seguir são executadas.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como um dos valores na tabela a seguir, de acordo com o valor da *KeysetSize* argumento **SQLSetScrollOptions**.  
  
    |*KeysetSize* argumento|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Um valor maior que o *RowsetSize* argumento|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como o *simultaneidade* argumento **SQLSetScrollOptions**.  
  
-   Se o *KeysetSize* argumentos na chamada para **SQLSetScrollOptions** for positivo, uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como o *KeysetSize* argumento **SQLSetScrollOptions**.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como o *RowsetSize* argumento **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Quando o Gerenciador de Driver mapeia **SQLSetScrollOptions** para um aplicativo trabalhando com um ODBC 3*. x* driver não oferece suporte a **SQLSetScrollOptions**, o Driver Manager define a opção de instrução SQL_ROWSET_SIZE, não o atributo SQL_ATTR_ROW_ARRAY_SIZE instrução para o *RowsetSize* argumento **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente quando a busca de várias linhas por uma chamada para **SQLExtendedFetch**.
