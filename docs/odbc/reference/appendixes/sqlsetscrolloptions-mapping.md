---
title: Mapeamento de SQLSetScrollOptions | Microsoft Docs
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
ms.openlocfilehash: 06b6b0f982b5c8d864e5024c8544f1f8e9af75ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091701"
---
# <a name="sqlsetscrolloptions-mapping"></a>Mapeamento SQLSetScrollOptions
Quando um aplicativo chama **SQLSetScrollOptions** por meio de um driver ODBC *3. x* e o driver não dá suporte a **SQLSetScrollOptions**, a chamada para  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 o resultado será o seguinte:  
  
-   Uma chamada para  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     com o argumento *InfoType* definido como um dos valores na tabela a seguir, dependendo do valor do argumento *keydefinem* em **SQLSetScrollOptions**.  
  
    |*Argumento Keydefine*|*Argumento InfoType*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |Um valor maior que o argumento de *conjunto* de linhas|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     Se o valor do argumento *Keydefinete* não estiver listado na tabela anterior, a chamada para **SQLSetScrollOptions** retornará SQLSTATE S1107 (valor de linha fora do intervalo) e nenhuma das etapas a seguir será executada.  
  
     Em seguida, o Gerenciador de driver verifica se o bit apropriado está definido no valor **InfoValuePtr* retornado pela chamada para **SQLGetInfo**, de acordo com o valor do argumento de *simultaneidade* em **SQLSetScrollOptions**.  
  
    |Argumento de *simultaneidade*|Configuração do *InfoType*|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     Se o argumento de *simultaneidade* não for um dos valores na tabela anterior, a chamada para **SQLSetScrollOptions** retornará SQLSTATE S1108 (opção de simultaneidade fora do intervalo) e nenhuma das etapas a seguir será executada. Se o bit apropriado (conforme indicado na tabela anterior) não estiver definido em **InfoValuePtr* para um dos valores correspondentes ao argumento *Concurrency* , a chamada para **SQLSetScrollOptions** retornará SQLSTATE S1C00 (driver não compatível) e nenhuma das etapas a seguir será executada.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como um dos valores na tabela a seguir, de acordo com o valor do argumento *keydefinem* em **SQLSetScrollOptions**.  
  
    |Argumento *Keydefine*|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |Um valor maior que o argumento de *conjunto* de linhas|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como o argumento de *simultaneidade* em **SQLSetScrollOptions**.  
  
-   Se o argumento *Keydefinete* na chamada para **SQLSetScrollOptions** for positivo, uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido como o argumento *keydefinete* em **SQLSetScrollOptions**.  
  
-   Uma chamada para  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     com * \*ValuePtr* definido *para o argumento de conjunto de* linhas em **SQLSetScrollOptions**.  
  
    > [!NOTE]  
    >  Quando o Gerenciador de driver mapeia o **SQLSetScrollOptions** para um aplicativo que trabalha com um driver ODBC *3. x* que não dá suporte a **SQLSetScrollOptions**, o Gerenciador de Driver define a opção de instrução SQL_ROWSET_SIZE, não o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE, para o argumento de *conjunto* em **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente ao buscar várias linhas por uma chamada para **SQLExtendedFetch**.
