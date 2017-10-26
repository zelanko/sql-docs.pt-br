---
title: Faz o Gerenciador de Driver | Microsoft Docs
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
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64c6fb04fe5c5c693da4982e1c12194bc7e42f98
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-manager-does"></a>O que faz o Gerenciador de Driver
A tabela a seguir resume como o ODBC 3*. x* Gerenciador de Driver mapeia chamadas para ODBC 2.* x* e o ODBC 3*. x* drivers.  
  
|Função ou<br /><br /> atributo de instrução|Comentários|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Aponta para o indicador a ser usado com **SQLFetchScroll**. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo define isso em um ODBC 2. *x* driver, o ODBC 3*. x* Gerenciador de Driver armazena em cache. Ele cancelará o ponteiro e passa o valor para o ODBC 2. *x* driver no *FetchOffset* argumento de **SQLExtendedFetch** quando **SQLFetchScroll** posterior é chamado pelo aplicativo.<br />-Quando um aplicativo define isso em um ODBC 3*. x* driver, o ODBC 3*. x* Gerenciador de Driver passará a chamada para o driver.|  
|SQL_ATTR_ROW_STATUS_PTR|Aponta para a matriz de status de linha preenchida por **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, e **SQLSetPos**. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo define isso em um ODBC 2. *x* driver, o ODBC 3*. x* Gerenciador de Driver armazena em cache em seu valor. Ele passa esse valor para o ODBC 2. *x* driver no *RowStatusArray* argumento de **SQLExtendedFetch** quando **SQLFetchScroll** ou **SQLFetch** é chamado.<br />-Quando um aplicativo define isso em um ODBC 3*. x* driver, o ODBC 3*. x* Gerenciador de Driver passará a chamada para o driver.<br />-No estado S6, se um aplicativo define SQL_ATTR_ROW_STATUS_PTR e, em seguida, chama **SQLBulkOperations** (com um *operação* de SQL_ADD) ou **SQLSetPos** sem primeiro chamar **SQLFetch** ou **SQLFetchScroll**, SQLSTATE HY011 (atributo não pode ser definido agora) será retornado.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Aponta para o buffer no qual **SQLFetch** e **SQLFetchScroll** retornar o número de linhas buscadas. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo define isso em um ODBC 2. *x* driver, o ODBC 3*. x* Gerenciador de Driver armazena em cache em seu valor. Ele passa esse valor para o ODBC 2. *x* driver no *RowCountPtr* argumento de **SQLExtendedFetch** quando **SQLFetch** ou **SQLFetchScroll** é chamado pelo aplicativo.<br />-Quando um aplicativo define isso em um ODBC 3*. x* driver, o ODBC 3*. x* Gerenciador de Driver passará a chamada para o driver.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Define o tamanho do conjunto de linhas. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo define isso em um ODBC 2. *x* driver, o ODBC 3*. x* Gerenciador de Driver mapeia para o atributo de instrução SQL_ROWSET_SIZE.<br />-Quando um aplicativo define isso em um ODBC 3*. x* driver, o ODBC 3*. x* Gerenciador de Driver passará a chamada para o driver.<br />-Quando um aplicativo trabalhando com um ODBC 3*. x* driver chama **SQLSetScrollOptions**, SQL_ROWSET_SIZE é definido como o valor de *RowsetSize* argumento se subjacente não oferece suporte a driver **SQLSetScrollOptions**.|  
|SQL_ROWSET_SIZE|Define o tamanho do conjunto de linhas usado por **SQLExtendedFetch** quando **SQLExtendedFetch** é chamado por um ODBC 2*. x* aplicativo. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo, define o ODBC 3*. x* Gerenciador de Driver passará a chamada para o driver, independentemente da versão do driver.<br />-Quando um aplicativo trabalhando com um ODBC 2. *x* driver chama **SQLSetScrollOptions**, SQL_ROWSET_SIZE é definido como o valor de **RowsetSize** argumento.|  
|**SQLBulkOperations**|Executa um inserir operação ou atualizar, excluir ou busca por operações de indicador. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLBulkOperations** com um *operação* de SQL_ADD em um ODBC 2.* x* driver, o ODBC 3*. x* Gerenciador de Driver mapeia para **SQLSetPos** com um *operação* de SQL_ADD.<br />-Quando estiver trabalhando com um ODBC 2. *x* driver não oferece suporte a **SQLSetPos** com um *operação* de SQL_ADD, o ODBC 3*. x* Gerenciador de Driver não mapear **SQLSetPos** com um *operação* de SQL_ADD para **SQLBulkOperations** com um *operação* de SQL_ADD. Isso ocorre porque **SQLBulkOperations** não pode ser chamado no estado S7, que no ODBC 2.* x* era o único estado no qual **SQLSetPos** poderia ser chamado.<br />-Se o aplicativo chama **SQLBulkOperations** com um *operação* de SQL_ADD em um ODBC 2.* x* driver antes de chamar **SQLFetchScroll**, o ODBC 3*. x* Gerenciador de Driver retornará um erro.|  
|**SQLExtendedFetch**|Retorna o conjunto de linhas especificado. Exceto para a restrição apenas observada, o ODBC 3*. x* Gerenciador de Driver passa chamadas para **SQLExtendedFetch** para o driver, independentemente da versão do driver.|  
|**SQLFetch**|Retorna o próximo conjunto de linhas. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLFetch** em um ODBC 2.* x* driver, o ODBC 3*. x* Gerenciador de Driver mapeia para **SQLExtendedFetch**. O *FetchOrientation* argumento de **SQLExtendedFetch** é definido como SQL_FETCH_NEXT. O Gerenciador de Driver usará o valor armazenado em cache do atributo de instrução SQL_ATTR_ROW_STATUS_PTR para o *RowStatusArray* argumento e o valor armazenado em cache do atributo SQL_ATTR_ROWS_FETCHED_PTR de instrução para o * RowCountPtr* argumento.<br />-Um ODBC 3*. x* aplicativo pode misturar chamadas para **SQLFetch** e **SQLFetchScroll** em um ODBC 2.* x* driver porque o ODBC 3*. x* mapeia o Gerenciador de Driver **SQLFetch** para **SQLExtendedFetch** quando um aplicativo chama-o em um ODBC 2.* x* driver.<br />-Se um ODBC 2. *x* não oferece suporte a driver **SQLExtendedFetch**, o ODBC 3*. x* Gerenciador de Driver não mapear **SQLFetch** ou ** SQLFetchScroll** para **SQLExtendedFetch** quando um aplicativo chama no driver. Se o aplicativo tenta defina SQL_ATTR_ROW_ARRAY_SIZE como um valor maior que 1, o SQLSTATE HYC00 (recurso opcional não implementado) será retornado.<br />-Exceto para as restrições apenas, o ODBC 3*. x* Gerenciador de Driver passa chamadas para **SQLFetch** para o driver, independentemente da versão do driver.|  
|**SQLFetchScroll**|Retorna o conjunto de linhas especificado. A seguir estão os detalhes de implementação:<br /><br /> -Quando um aplicativo chama **SQLFetchScroll** em um ODBC 2.* x* driver, o ODBC 3*. x* Gerenciador de Driver mapeia para **SQLExtendedFetch**. Ele usa o valor armazenado em cache do atributo de instrução SQL_ATTR_ROW_STATUS_PTR para o *RowStatusArray* argumento e o valor armazenado em cache do atributo SQL_ATTR_ROWS_FETCHED_PTR de instrução para o *RowCountPtr* argumento. Se o *FetchOrientation* argumento **SQLFetchScroll** é SQL_FETCH_BOOKMARK, ele usa o valor armazenado em cache do atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR para o *FetchOffset * argumento e retorna um erro se o *FetchOffset* argumento de **SQLFetchScroll** é não em 0.<br />-Quando um aplicativo chama isso em um ODBC 3*. x* driver, o ODBC 3*. x* Gerenciador de Driver passará a chamada para o driver.|  
|**SQLSetPos**|Executa várias operações posicionadas. O ODBC 3*. x* Gerenciador de Driver passa chamadas para **SQLSetPos** para o driver, independentemente da versão do driver.|  
|**SQLSetScrollOptions**|Quando o Gerenciador de Driver mapeia **SQLSetScrollOptions** para um aplicativo trabalhando com um ODBC 3*. x* driver não oferece suporte a **SQLSetScrollOptions**, o Driver Manager define a opção de instrução SQL_ROWSET_SIZE, não o atributo SQL_ATTR_ROW_ARRAY_SIZE instrução para o *RowsetSize* argumento **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente quando a busca de várias linhas por uma chamada para **SQLExtendedFetch**.|

