---
title: O que faz o Driver | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c4c1bf17e8a54f4eeb8722b1a17b9e85b930dd00
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="what-the-driver-does"></a>O que faz o Driver
A tabela a seguir resume quais funções e um ODBC 3 de atributos de instrução*. x* driver deve implementar para bloquear e cursores roláveis.  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Define o endereço da matriz de status de linha preenchido por **SQLFetch** e **SQLFetchScroll**. Essa matriz também é preenchida por **SQLSetPos** se **SQLSetPos** é chamado no estado de instrução S6. Se **SQLSetPos** é chamado no estado S7, essa matriz não está preenchida, mas a matriz apontada pelo *RowStatusArray* argumento de **SQLExtendedFetch** é preenchido. Para obter mais informações, consulte [instrução transições](../../../odbc/reference/appendixes/statement-transitions.md) nas tabelas de transição de estado do apêndice b: ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Define o endereço do buffer no qual **SQLFetch** e **SQLFetchScroll** retornar o número de linhas buscadas. Se **SQLExtendedFetch** é chamado, esse buffer não está preenchido, mas o *RowCountPtr* argumento aponta para o número de linhas buscadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas usado por **SQLFetch** e **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Define o tamanho do conjunto de linhas usado por **SQLExtendedFetch**. ODBC 3*. x* drivers implementam isso, se desejar trabalhar com ODBC 2. *x* aplicativos que chamam **SQLExtendedFetch** ou **SQLSetPos**.|  
|**SQLBulkOperations**|Se um ODBC 3*. x* driver deve funcionar com ODBC 2. *x* aplicativos que usam **SQLSetPos** com um *operação* de SQL_ADD, o driver deve oferecer suporte **SQLSetPos** com um  *Operação* de SQL_ADD além **SQLBulkOperations** com um *operação* de SQL_ADD.|  
|**SQLExtendedFetch**|Retorna o conjunto de linhas especificado. ODBC 3*. x* drivers implementam isso, se desejar trabalhar com ODBC 2. *x* aplicativos que chamam **SQLExtendedFetch** ou **SQLSetPos**. A seguir estão os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do valor do atributo de instrução SQL_ROWSET_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do *RowStatusArray* argumento, não o atributo da instrução SQL_ATTR_ROW_STATUS_PTR. O *RowStatusArray* argumento em uma chamada para **SQLExtendedFetch** não deve ser um ponteiro nulo. (Observe que no ODBC 3*. x*, o atributo da instrução sql_attr_row_status_ptr de modo que pode ser um ponteiro nulo.)<br />-O driver recupera o endereço do buffer de linhas buscadas o *RowCountPtr* argumento, não o atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O driver retornará SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLExtendedFetch**. Um ODBC 3*. x* driver deve retornar SQLSTATE 01S01 (erro na linha) somente quando **SQLExtendedFetch** é chamado, não quando **SQLFetch** ou **SQLFetchScroll** é chamado. Para preservar a compatibilidade com versões anteriores, quando SQLSTATE 01S01 (erro na linha) é retornado por **SQLExtendedFetch**, o Gerenciador de Driver não ordena os registros de status na fila de erros de acordo com as regras mencionadas no "sequência de Status Registros"seção [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. A seguir estão os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do valor do atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-O driver recupera o endereço de linhas buscadas buffer do atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O aplicativo pode misturar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-   **SQLFetch** retorna indicadores se a coluna 0 está associada.<br />-   **SQLFetch** pode ser chamado para retornar mais de uma linha.<br />-O driver não retorna um SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetch**.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. A seguir estão os detalhes de implementação:<br /><br /> -O driver recupera o tamanho do conjunto de linhas do atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE.<br />-O driver recupera o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-O driver recupera o endereço de linhas buscadas buffer do atributo de instrução SQL_ATTR_ROWS_FETCHED_PTR.<br />-O aplicativo pode misturar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-O driver não retorna um SQLSTATE 01S01 (erro na linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetchScroll**.|  
|**SQLSetPos**|Executa várias operações posicionadas. A seguir estão os detalhes de implementação:<br /><br /> -Isso pode ser chamado em estados de instrução S6 ou S7. Para obter mais detalhes, consulte [instrução transições](../../../odbc/reference/appendixes/statement-transitions.md) nas tabelas de transição de estado do apêndice b: ODBC.<br />-Se isso é chamado em um estado de instrução S5 ou S6, o driver recupera o tamanho do conjunto de linhas do atributo de instrução de SQL_ATTR_ROWS_FETCHED_PTR e o endereço da matriz de status de linha do atributo de instrução SQL_ATTR_ROW_STATUS_PTR.<br />-Se isso é chamado no estado de instrução S7, o driver recupera o tamanho do conjunto de linhas do atributo de instrução SQL_ROWSET_SIZE e o endereço da matriz de status de linha do *RowStatusArray* argumento de  **SQLExtendedFetch**.<br />-O driver retornará SQLSTATE 01S01 (erro na linha) apenas para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLSetPos** para executar uma operação em massa quando a função é chamada no estado S7. Para preservar a compatibilidade com versões anteriores, se SQLSTATE 01S01 (erro na linha) é retornado por **SQLSetPos**, o Gerenciador de Driver não ordena os registros de status na fila de erros de acordo com as regras mencionadas "Sequência de registro de Status" seção de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />-Se o driver deve trabalhar com ODBC 2. *x* aplicativos que chamam **SQLSetPos** com um *operação* argumento de SQL_ADD, o driver deve oferecer suporte **SQLSetPos** com um  *Operação* argumento de SQL_ADD.|
