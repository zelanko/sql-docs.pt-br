---
title: Rolando e buscando linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c31b5a4d086fec3ac3db6e3eb1bfbd6bf54c8cb3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006338"
---
# <a name="scrolling-and-fetching-rows"></a>Rolando e buscando linhas
  Para usar um cursor rolável, um aplicativo ODBC deve:  
  
-   Definir os recursos do cursor usando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Abrir o cursor usando **SQLExecute** ou **SQLExecDirect**.  
  
-   Rolar e buscar linhas usando **SQLFetch** ou [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md).  
  
 Ambos **SQLFetch** e **SQLFetchSroll** pode buscar blocos de linhas por vez. O número de linhas retornadas é especificado usando **SQLSetStmtAttr** para definir o parâmetro SQL_ATTR_ROW_ARRAY_SIZE.  
  
 Aplicativos ODBC podem usar **SQLFetch** para buscar por um cursor somente de avanço.  
  
 **SQLFetchScroll** é usado para rolar ao redor de um cursor. **SQLFetchScroll** dá suporte à busca o próximo, anterior, primeiro e últimos conjuntos de linhas além da busca relativa (busque *n* linhas desde o início do conjunto de linhas atual) e busca absoluta (busca o conjunto de linhas começando na linha *n*). Se *n* é negativo em uma busca absoluta, as linhas são contadas do final do conjunto de resultados. Uma busca absoluta da linha -1 significa buscar o conjunto de linhas que inicia com a última linha no conjunto de resultados.  
  
 Aplicativos que usam **SQLFetchScroll** apenas para seu bloco funcionalidades de cursor, como relatórios, provavelmente serão passar pelo conjunto de resultados de uma única vez, usando apenas a opção para buscar o próximo conjunto de linhas. Aplicativos baseados em tela, por outro lado, podem tirar proveito dos recursos do **SQLFetchScroll**. Se o aplicativo define o tamanho do conjunto de linhas para o número de linhas exibidas na tela e associa os buffers de tela ao conjunto de resultados, ele poderá converter operações da barra de rolagem diretamente em chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Página abaixo|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com FetchOffset igual a -1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com FetchOffset igual a 1|  
|Caixa de rolagem no início|SQL_FETCH_FIRST|  
|Caixa de rolagem no fim|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Indicando linhas em ODBC](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Consulte também  
 [Usar cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  