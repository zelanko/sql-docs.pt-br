---
title: Rolagem e Busca de Linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ae9f1079f329951045d4b3f61b39c12efc153fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302481"
---
# <a name="scrolling-and-fetching-rows"></a>Rolando e buscando linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para usar um cursor rolável, um aplicativo ODBC deve:  
  
-   Defina os recursos do cursor usando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Abra o cursor usando **SQLExecute** ou **SQLExecDirect**.  
  
-   Role e busque linhas usando **SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 Tanto **o SQLFetch** quanto **o SQLFetchSroll** podem buscar blocos de linhas de cada vez. O número de linhas retornadas é especificado usando **SQLSetStmtAttr** para definir o parâmetro SQL_ATTR_ROW_ARRAY_SIZE.  
  
 Os aplicativos ODBC podem usar **o SQLFetch** para buscar através de um cursor somente para frente.  
  
 **SQLFetchScroll** é usado para rolar em torno de um cursor. **SQLFetchScroll** suporta buscar os próximos, anteriores, primeiros e últimos conjuntos de linhas, além de busca relativa (buscar as linhas de linha *n* do início do conjunto de linhas atuais) e busca absoluta (buscar o conjunto de linhas a partir da linha *n*). Se *n* for negativo em uma busca absoluta, as linhas são contadas a partir do final do conjunto de resultados. Uma busca absoluta da linha -1 significa buscar o conjunto de linhas que inicia com a última linha no conjunto de resultados.  
  
 Os aplicativos que usam **sqlfetchscroll** apenas para seus recursos de cursor de bloco, como relatórios, provavelmente passarão pelo conjunto de resultados uma única vez, usando apenas a opção de buscar o próximo conjunto de linhas. Aplicativos baseados em tela, por outro lado, podem tirar proveito de todos os recursos do **SQLFetchScroll**. Se o aplicativo definir o tamanho do conjunto de linhas para o número de linhas exibidas na tela e vincular os buffers de tela ao conjunto de resultados, ele poderá traduzir as operações da barra de rolagem diretamente para chamadas para **SQLFetchScroll**.  
  
|Operação de barra de rolagem|Opção de rolagem SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Uma página acima|SQL_FETCH_PRIOR|  
|Página para baixo|SQL_FETCH_NEXT|  
|Uma linha acima|SQL_FETCH_RELATIVE com FetchOffset igual a -1|  
|Uma linha abaixo|SQL_FETCH_RELATIVE com FetchOffset igual a 1|  
|Caixa de rolagem no início|SQL_FETCH_FIRST|  
|Caixa de rolagem no fim|SQL_FETCH_LAST|  
|Posição aleatória da caixa de rolagem|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Indicando linhas em ODBC](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Usando cursors &#40;&#41;ODBC](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
