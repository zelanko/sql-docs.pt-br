---
title: Rolagem e busca de linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
author: rothja
ms.author: jroth
ms.openlocfilehash: 08e7f37818ab8a1695e21bae527afc633a2b69c5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020393"
---
# <a name="scrolling-and-fetching-rows"></a>Rolando e buscando linhas
  Para usar um cursor rolável, um aplicativo ODBC deve:  
  
-   Defina os recursos de cursor usando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Abra o cursor usando **SQLExecute** ou **SQLExecDirect**.  
  
-   Role e busque linhas usando **SQLFetch** ou [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md).  
  
 **SQLFetch** e **SQLFetchSroll** podem buscar blocos de linhas por vez. O número de linhas retornadas é especificado usando **SQLSetStmtAttr** para definir o parâmetro SQL_ATTR_ROW_ARRAY_SIZE.  
  
 Os aplicativos ODBC podem usar **SQLFetch** para buscar por meio de um cursor de somente avanço.  
  
 **SQLFetchScroll** é usado para rolar em um cursor. O **SQLFetchScroll** dá suporte à busca dos próximos conjuntos de linhas, antes, primeiro e último, além da busca relativa (busque o conjunto de linha *n* linhas do início do conjunto de linhas atual) e a busca absoluta (busque o conjunto de linhas começando na linha *n*). Se *n* for negativo em uma busca absoluta, as linhas serão contadas a partir do final do conjunto de resultados. Uma busca absoluta da linha -1 significa buscar o conjunto de linhas que inicia com a última linha no conjunto de resultados.  
  
 Os aplicativos que usam **SQLFetchScroll** apenas para seus recursos de cursor de bloco, como relatórios, provavelmente passarão pelo conjunto de resultados uma única vez, usando apenas a opção para buscar o próximo conjunto de linhas. Os aplicativos baseados em tela, por outro lado, podem tirar proveito de todos os recursos do **SQLFetchScroll**. Se o aplicativo definir o tamanho do conjunto de linhas como o número de linhas exibidas na tela e associar os buffers de tela ao conjunto de resultados, ele poderá converter as operações da barra de rolagem diretamente em chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Page Down|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com FetchOffset igual a-1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com FetchOffset igual a 1|  
|Caixa de rolagem no início|SQL_FETCH_FIRST|  
|Caixa de rolagem no fim|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Indicando linhas em ODBC](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Usando cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
