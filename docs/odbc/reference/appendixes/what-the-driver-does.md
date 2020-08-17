---
description: O que o driver faz
title: O que o driver faz | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f15473d1eb0e6344fbd5772f2b28233c07aa7a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386222"
---
# <a name="what-the-driver-does"></a>O que o driver faz
A tabela a seguir resume quais funções e atributos de instrução um driver ODBC *3. x* deve implementar para cursores de bloco e rolável.  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Define o endereço da matriz de status de linha preenchida por **SQLFetch** e **SQLFetchScroll**. Essa matriz também será preenchida por **SQLSetPos** se **SQLSetPos** for chamado no estado de instrução s6. Se **SQLSetPos** for chamado no estado S7, essa matriz não será preenchida, mas a matriz apontada pelo argumento *RowStatusArray* de **SQLExtendedFetch** será preenchida. Para obter mais informações, consulte as [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: tabelas de transição de estado ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Define o endereço do buffer no qual **SQLFetch** e **SQLFetchScroll** retornam o número de linhas buscadas. Se **SQLExtendedFetch** for chamado, esse buffer não será preenchido, mas o argumento *RowCountPtr* apontará para o número de linhas buscadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas usado por **SQLFetch** e **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Define o tamanho do conjunto de linhas usado por **SQLExtendedFetch**. Os drivers ODBC *3. x* implementam isso se desejarem trabalhar com aplicativos ODBC *2. x* que chamam **SQLExtendedFetch** ou **SQLSetPos**.|  
|**SQLBulkOperations**|Se um driver ODBC *3. x* funcionar com aplicativos ODBC *2. x* que usam **SQLSetPos** com uma *operação* de SQL_ADD, o driver deverá dar suporte a **SQLSetPos** com uma *operação* de SQL_ADD além do **SQLBulkOperations** com uma *operação* de SQL_ADD.|  
|**SQLExtendedFetch**|Retorna o conjunto de linhas especificado. Os drivers ODBC *3. x* implementam isso se desejarem trabalhar com aplicativos ODBC *2. x* que chamam **SQLExtendedFetch** ou **SQLSetPos**. Veja a seguir os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do valor do atributo da instrução SQL_ROWSET_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do argumento *RowStatusArray* , não o atributo de instrução SQL_ATTR_ROW_STATUS_PTR. O argumento *RowStatusArray* em uma chamada para **SQLExtendedFetch** não deve ser um ponteiro nulo. (Observe que no ODBC *3. x*, o atributo da instrução SQL_ATTR_ROW_STATUS_PTR pode ser um ponteiro nulo.)<br />-O driver recupera o endereço do buffer de linhas buscados do argumento *RowCountPtr* , não o atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O driver retorna SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLExtendedFetch**. Um driver ODBC *3. x* deve retornar SQLSTATE 01S01 (Error na linha) somente quando **SQLExtendedFetch** for chamado, não quando **SQLFetch** ou **SQLFetchScroll** for chamado. Para preservar a compatibilidade com versões anteriores, quando SQLSTATE 01S01 (erro na linha) é retornado por **SQLExtendedFetch**, o Gerenciador de driver não ordena os registros de status na fila de erros de acordo com as regras declaradas na seção "sequência de registros de status" de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. Veja a seguir os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do valor do atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-O driver recupera o endereço do buffer de linhas buscados do atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O aplicativo pode misturar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-   **SQLFetch** retornará indicadores se a coluna 0 estiver associada.<br />-   **SQLFetch** pode ser chamado para retornar mais de uma linha.<br />-O driver não retorna SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetch**.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. Veja a seguir os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-O driver recupera o endereço do buffer de linhas buscados do atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O aplicativo pode misturar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-O driver não retorna SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetchScroll**.|  
|**SQLSetPos**|Executa várias operações posicionadas. Veja a seguir os detalhes de implementação:<br /><br /> -Isso pode ser chamado nos Estados de instrução S6 ou S7. Para obter mais detalhes, consulte as [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: tabelas de transição de estado ODBC.<br />-Se for chamado no estado da instrução S5 ou S6, o driver recuperará o tamanho do conjunto de linhas do atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR e o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-Se for chamado no estado da instrução S7, o driver recuperará o tamanho do conjunto de linhas do atributo da instrução SQL_ROWSET_SIZE e o endereço da matriz de status de linha do argumento *RowStatusArray* de **SQLExtendedFetch**.<br />-O driver retorna SQLSTATE 01S01 (erro na linha) apenas para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLSetPos** para executar uma operação em massa quando a função é chamada no estado S7. Para preservar a compatibilidade com versões anteriores, se SQLSTATE 01S01 (erro na linha) for retornado por **SQLSetPos**, o Gerenciador de driver não ordenará os registros de status na fila de erros de acordo com as regras indicadas na seção "sequência de registros de status" de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />-Se o driver funcionar com aplicativos ODBC *2. x* que chamam **SQLSetPos** com um argumento de *operação* de SQL_ADD, o driver deverá dar suporte a **SQLSetPos** com um argumento de *operação* de SQL_ADD.|
