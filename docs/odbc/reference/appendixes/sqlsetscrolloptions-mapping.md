---
title: Mapeamento SQLSetScrollOptions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5520554b509b0c25d62e4a191e16ad3524a02652
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651434"
---
# <a name="sqlsetscrolloptions-mapping"></a>Mapeamento SQLSetScrollOptions
Quando um aplicativo chama **SQLSetScrollOptions** por meio de um ODBC 3 *. x* driver e o driver não oferece suporte **SQLSetScrollOptions**, a chamada para  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 resulta da seguinte maneira:  
  
-   Uma chamada para  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     com o *tipo de informação* argumento definido como um dos valores na tabela a seguir, dependendo do valor da *KeysetSize* argumento **SQLSetScrollOptions**.  
  
    |*Argumento KeysetSize*|*Argumento de tipo de informação*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Um valor maior que o *RowsetSize* argumento|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Se o valor da *KeysetSize* argumento não estiver listado na tabela anterior, a chamada para **SQLSetScrollOptions** retornará SQLSTATE S1107 (valor fora do intervalo de linha) e nenhuma das etapas a seguir é executada.  
  
     O Gerenciador de Driver, em seguida, verifica se o bit apropriado está definido no **InfoValuePtr* valor retornado pela chamada para **SQLGetInfo**, acordo com o valor da *simultaneidade* argumento na **SQLSetScrollOptions**.  
  
    |*Simultaneidade* argumento|*Tipo de informação* configuração|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Se o *simultaneidade* argumento não é um dos valores na tabela anterior, a chamada para **SQLSetScrollOptions** retornará SQLSTATE S1108 (opção de simultaneidade fora do intervalo) e nenhuma das etapas a seguir é executada. Se o bit apropriado (conforme indicado na tabela anterior) não está definido **InfoValuePtr* a um dos valores correspondentes para o *simultaneidade* argumento, a chamada para  **SQLSetScrollOptions** retornará SQLSTATE S1C00 (não têm a capacidade de Driver), e nenhuma das etapas a seguir são executadas.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     com o  *\*ValuePtr* definido como um dos valores na tabela a seguir, o valor de acordo com ao *KeysetSize* argumento na **SQLSetScrollOptions**.  
  
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
  
     com o  *\*ValuePtr* definido como o *simultaneidade* argumento na **SQLSetScrollOptions**.  
  
-   Se o *KeysetSize* argumento na chamada para **SQLSetScrollOptions** for positivo, uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     com o  *\*ValuePtr* definido como o *KeysetSize* argumento na **SQLSetScrollOptions**.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     com o  *\*ValuePtr* definido como o *RowsetSize* argumento na **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Quando o Gerenciador de Driver mapeia **SQLSetScrollOptions** para um aplicativo trabalhar com um ODBC 3 *. x* que não oferece suporte a driver **SQLSetScrollOptions**, o Driver Manager define a opção de instrução SQL_ROWSET_SIZE, não o atributo SQL_ATTR_ROW_ARRAY_SIZE instrução para o *RowsetSize* argumento **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente quando ao buscar várias linhas por uma chamada para **SQLExtendedFetch**.
