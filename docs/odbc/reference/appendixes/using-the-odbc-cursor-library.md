---
description: Usar a biblioteca de cursores ODBC
title: Usando a biblioteca de cursores ODBC | Microsoft Docs
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
ms.openlocfilehash: be42c95692537c0479afb7ed492756b8a54ab030
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386192"
---
# <a name="using-the-odbc-cursor-library"></a>Usar a biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para usar a biblioteca de cursores ODBC, um aplicativo:  
  
1.  Chama **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_ODBC_CURSORS para especificar como a biblioteca de cursores deve ser usada com uma conexão específica. A biblioteca de cursores pode ser sempre usada (SQL_CUR_USE_ODBC), usada somente se o driver não der suporte a cursores roláveis (SQL_CUR_USE_IF_NEEDED) ou nunca usado (SQL_CUR_USE_DRIVER).  
  
2.  Chama **SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect** para se conectar à fonte de dados.  
  
3.  Chama **SQLSetStmtAttr** para especificar o tipo de cursor (SQL_ATTR_CURSOR_TYPE), simultaneidade (SQL_ATTR_CONCURRENCY) e tamanho do conjunto de linhas (SQL_ATTR_ROW_ARRAY_SIZE). A biblioteca de cursores dá suporte a cursores estáticos e somente de encaminhamento. Cursores somente de avanço devem ser somente leitura, enquanto cursores estáticos podem ser somente leitura ou podem usar o controle de simultaneidade otimista comparando valores.  
  
4.  Aloca um ou mais buffers de conjunto de linhas e chama **SQLBindCol** uma ou mais vezes para associar esses buffers às colunas do conjunto de resultados.  
  
5.  Gera um conjunto de resultados executando uma instrução **Select** ou um procedimento, ou chamando uma função de catálogo. Se o aplicativo for executar instruções UPDATE posicionadas, ele deverá executar uma instrução **SELECT for Update** para gerar o conjunto de resultados.  
  
6.  Chama **SQLFetch** ou **SQLFetchScroll** uma ou mais vezes para rolar pelo conjunto de resultados.  
  
 O aplicativo pode alterar os valores de dados nos buffers de conjunto de linhas. Para atualizar os buffers de conjunto de linhas com dados do cache da biblioteca de cursores, um aplicativo chama **SQLFetchScroll** com o argumento *FetchOrientation* definido como SQL_FETCH_RELATIVE e o argumento *FetchOffset* definido como 0.  
  
 Para recuperar dados de uma coluna desassociada, o aplicativo chama **SQLSetPos** para posicionar o cursor na linha desejada. Em seguida, ele chama **SQLGetData** para recuperar os dados.  
  
 Para determinar o número de linhas que foram recuperadas da fonte de dados, o aplicativo chama **SQLRowCount**.
