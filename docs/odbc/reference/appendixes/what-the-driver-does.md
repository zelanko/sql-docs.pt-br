---
title: O que o motorista faz | Microsoft Docs
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
ms.openlocfilehash: c0438478f5aa625ffdd4d3bcd1c0a6f0f80d3367
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301387"
---
# <a name="what-the-driver-does"></a>O que o driver faz
A tabela a seguir resume quais funções e atributos de declaração um driver ODBC *3.x* deve implementar para cursores de bloco e roláveis.  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Define o endereço da matriz de status da linha preenchida por **SQLFetch** e **SQLFetchScroll**. Esta matriz também é preenchida por **SQLSetPos** se **SQLSetPos** for chamado no estado de declaração S6. Se **SQLSetPos** for chamado no estado S7, esta matriz não será preenchida, mas a matriz apontada pelo argumento *RowStatusArray* do **SQLExtendedFetch** será preenchida. Para obter mais informações, consulte [Transições de Declaração](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: Tabelas de transição do estado ODBC.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Define o endereço do buffer no qual **SQLFetch** e **SQLFetchScroll** retornam o número de linhas buscadas. Se **SQLExtendedFetch** for chamado, este buffer não será preenchido, mas o argumento *RowCountPtr* aponta para o número de linhas buscadas.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas usado por **SQLFetch** e **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE|Define o tamanho do conjunto de linhas usado por **SQLExtendedFetch**. Os drivers ODBC *3.x* implementam isso se quiserem trabalhar com aplicativos ODBC *2.x* que chamam **sQLExtendedFetch** ou **SQLSetPos**.|  
|**SQLBulkOperations**|Se um driver ODBC *3.x* trabalhar com aplicativos ODBC *2.x* que usam **SQLSetPos** com uma *Operação* de SQL_ADD, o driver deve suportar **SQLSetPos** com uma *operação* de SQL_ADD além **de SQLBulkOperations** com uma *Operação* de SQL_ADD.|  
|**Sqlextendedfetch**|Retorna o conjunto de linhas especificado. Os drivers ODBC *3.x* implementam isso se quiserem trabalhar com aplicativos ODBC *2.x* que chamam **sQLExtendedFetch** ou **SQLSetPos**. A seguir, os detalhes da implementação:<br /><br /> - O driver recupera o tamanho do conjunto de linhas do valor do atributo de declaração SQL_ROWSET_SIZE.<br />- O driver recupera o endereço da matriz de status da linha a partir do argumento *RowStatusArray,* não do atributo de declaração SQL_ATTR_ROW_STATUS_PTR. O argumento *RowStatusArray* em uma chamada para **SQLExtendedFetch** não deve ser um ponteiro nulo. (Observe que no ODBC *3.x*, o atributo de declaração SQL_ATTR_ROW_STATUS_PTR pode ser um ponteiro nulo.)<br />- O driver recupera o endereço das linhas buscadas buffer do argumento *RowCountPtr,* não o atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR.<br />- O driver retorna SQLSTATE 01S01 (Erro em linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLExtendedFetch**. Um driver ODBC *3.x* deve retornar SQLSTATE 01S01 (Erro na linha) somente quando **SQLExtendedFetch** for chamado, não quando **SQLFetch** ou **SQLFetchScroll** for chamado. Para preservar a compatibilidade retrógrada, quando o SQLSTATE 01S01 (Erro em linha) é devolvido pelo **SQLExtendedFetch,** o Driver Manager não encomenda registros de status na fila de erro de acordo com as regras indicadas na seção "Seqüência de Registros de Status" do [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. A seguir, os detalhes da implementação:<br /><br /> - O driver recupera o tamanho do conjunto de linhas do valor do atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE.<br />- O driver recupera o endereço da matriz de status da linha do atributo de declaração SQL_ATTR_ROW_STATUS_PTR.<br />- O motorista recupera o endereço das linhas obtidas no buffer do atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR.<br />- O aplicativo pode misturar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />-   **SQLFetch** retorna marcadores se a coluna 0 estiver vinculada.<br />-   **SQLFetch** pode ser chamado para retornar mais de uma linha.<br />- O driver não retorna SQLSTATE 01S01 (Erro em linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetch**.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. A seguir, os detalhes da implementação:<br /><br /> - O driver recupera o tamanho do conjunto de linhas do atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE.<br />- O driver recupera o endereço da matriz de status da linha do atributo de declaração SQL_ATTR_ROW_STATUS_PTR.<br />- O motorista recupera o endereço das linhas obtidas no buffer do atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR.<br />- O aplicativo pode misturar chamadas entre **SQLFetchScroll** e **SQLFetch**.<br />- O driver não retorna SQLSTATE 01S01 (Erro em linha) para indicar que ocorreu um erro enquanto as linhas foram buscadas por uma chamada para **SQLFetchScroll**.|  
|**SQLSetPos**|Realiza várias operações posicionadas. A seguir, os detalhes da implementação:<br /><br /> - Isso pode ser chamado nos estados de declaração S6 ou S7. Para obter mais detalhes, consulte [Transições de Declaração](../../../odbc/reference/appendixes/statement-transitions.md) no apêndice B: Tabelas de transição do estado ODBC.<br />- Se isso for chamado no estado de declaração S5 ou S6, o driver recuperará o tamanho do conjunto de linhas do atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR e o endereço da matriz de status da linha do atributo de declaração SQL_ATTR_ROW_STATUS_PTR.<br />- Se isso for chamado no estado de declaração S7, o driver recuperará o tamanho do conjunto de linhas do atributo de declaração SQL_ROWSET_SIZE e o endereço da matriz de status da linha a partir do argumento *RowStatusArray* do **SQLExtendedFetch**.<br />- O driver retorna SQLSTATE 01S01 (Erro na linha) apenas para indicar que ocorreu um erro enquanto as linhas foram solicitadas por uma chamada para **SQLSetPos** para realizar uma operação em massa quando a função é chamada no estado S7. Para preservar a compatibilidade retrógrada, se o SQLSTATE 01S01 (Erro em linha) for devolvido por **SQLSetPos,** o Driver Manager não solicitará registros de status na fila de erro de acordo com as regras indicadas na seção "Seqüência de Registros de Status" do [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />- Se o driver trabalhar com aplicativos ODBC *2.x* que chamam **sqlSetPos** com um argumento de *Operação* de SQL_ADD, o motorista deve suportar **SQLSetPos** com um argumento de *Operação* de SQL_ADD.|
