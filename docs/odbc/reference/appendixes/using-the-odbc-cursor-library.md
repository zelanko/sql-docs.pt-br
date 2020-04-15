---
title: Usando a Biblioteca Cursor ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c740ed78de51684eac38ad0c54ab2224986018d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301397"
---
# <a name="using-the-odbc-cursor-library"></a>Usar a biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Para usar a biblioteca do cursor ODBC, um aplicativo:  
  
1.  Chama **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_ODBC_CURSORS para especificar como a biblioteca do cursor deve ser usada com uma conexão específica. A biblioteca do cursor pode ser sempre usada (SQL_CUR_USE_ODBC), usada apenas se o driver não suportar cursores roláveis (SQL_CUR_USE_IF_NEEDED) ou nunca usado (SQL_CUR_USE_DRIVER).  
  
2.  Chama **SQLConnect,** **SQLDriverConnect**ou **SQLBrowseConnect** para se conectar à fonte de dados.  
  
3.  Chama **SQLSetStmtAttr** para especificar o tipo de cursor (SQL_ATTR_CURSOR_TYPE), a concorrência (SQL_ATTR_CONCURRENCY) e o tamanho do conjunto de linhas (SQL_ATTR_ROW_ARRAY_SIZE). A biblioteca do cursor suporta cursores estáticas e avançados. Os cursores somente para frente devem ser lidos, enquanto os cursores estáticos podem ser apenas leitura ou podem usar controle de concorrência otimista comparando valores.  
  
4.  Aloca um ou mais buffers de conjunto de linhas e chama **sqlBindCol** uma ou mais vezes para vincular esses buffers a colunas de conjunto de resultados.  
  
5.  Gera um conjunto de resultados executando uma declaração **SELECT** ou um procedimento, ou chamando uma função de catálogo. Se o aplicativo executar as instruções de atualização posicionadas, ele deverá executar uma instrução **SELECT FOR UPDATE** para gerar o conjunto de resultados.  
  
6.  Chama **SQLFetch** ou **SQLFetchScroll** uma ou mais vezes para percorrer o conjunto de resultados.  
  
 O aplicativo pode alterar os valores de dados nos buffers de conjunto de linhas. Para atualizar os buffers de conjunto de linhas com dados do cache da biblioteca do cursor, um aplicativo chama **SQLFetchScroll** com o argumento *FetchOrientation* definido para SQL_FETCH_RELATIVE e o argumento *FetchOffset* definido como 0.  
  
 Para recuperar dados de uma coluna não vinculada, o aplicativo chama **SQLSetPos** para posicionar o cursor na linha desejada. Em seguida, ele chama **SQLGetData** para recuperar os dados.  
  
 Para determinar o número de linhas que foram recuperadas da fonte de dados, o aplicativo chama **SQLRowCount**.
