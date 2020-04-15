---
title: Mapeamento de opções de SQLSetScroll | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77050df283b10abd17ba62a48bd366d6c1b3f601
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300496"
---
# <a name="sqlsetscrolloptions-mapping"></a>Mapeamento SQLSetScrollOptions
Quando um aplicativo chama **SQLSetScrollOptions** através de um driver ODBC *3.x* e o driver não suporta **SQLSetScrollOptions**, a chamada para  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 resultará da seguinte forma:  
  
-   Uma chamada para  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     com o argumento *InfoType* definido como um dos valores na tabela a seguir, dependendo do valor do argumento *KeysetSize* no **SQLSetScrollOptions**.  
  
    |*Argumento KeysetSize*|*Argumento InfoType*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Um valor maior do que o argumento *RowsetSize*|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Se o valor do argumento *KeysetSize* não estiver listado na tabela anterior, a chamada para **SQLSetScrollOptions** retorna SQLSTATE S1107 (valor da linha fora do alcance) e nenhuma das etapas a seguir será executada.  
  
     Em seguida, o Gerenciador de driver verifica se o bit apropriado está definido no valor ** InfoValuePtr* retornado pela chamada para **SQLGetInfo,** de acordo com o valor do argumento *Concurrency* no **SQLSetScrollOptions**.  
  
    |*Argumento de concorrência*|*Configuração infotype*|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Se o argumento *Concurrency* não for um dos valores na tabela anterior, a chamada para **SQLSetScrollOptions** retorna SQLSTATE S1108 (opção de concorrência fora do alcance) e nenhuma das etapas a seguir será executada. Se o bit apropriado (como indicado na tabela anterior) não estiver definido em **InfoValuePtr* para um dos valores correspondentes ao argumento *Concurrency,* a chamada para **SQLSetScrollOptions** retorna SQLSTATE S1C00 (Driver não é capaz) e nenhuma das seguintes etapas são executadas.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como um dos valores na tabela a seguir, de acordo com o valor do argumento *KeysetSize* no **SQLSetScrollOptions**.  
  
    |*Argumento KeysetSize*|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Um valor maior do que o argumento *RowsetSize*|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido para o argumento *Concurrency* em **SQLSetScrollOptions**.  
  
-   Se o argumento *KeysetSize* na chamada para **SQLSetScrollOptions** for positivo, uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido para o argumento *KeysetSize* em **SQLSetScrollOptions**.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido para o argumento *RowsetSize* em **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Quando o Gerenciador de driver mapeia **SQLSetScrollOptions** para um aplicativo que trabalha com um driver ODBC *3.x* que não suporta **SQLSetScrollOptions,** o Gerenciador de driver define a opção de declaração SQL_ROWSET_SIZE, não o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE, para o argumento *RowsetSize* no **SQLSetScrollOption**. Como resultado, **sqlsetscrolloptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele só pode ser usado quando busca várias linhas por uma chamada para **SQLExtendedFetch**.
