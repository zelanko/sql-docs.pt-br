---
title: Usando a biblioteca de cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7a620f26f8f62b4fc5189f7174dd9026968d169
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-the-odbc-cursor-library"></a>Usando a biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Para usar a biblioteca de cursores ODBC, um aplicativo:  
  
1.  Chamadas **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_ODBC_CURSORS para especificar como a biblioteca de cursores deve ser usada com uma conexão específica. A biblioteca de cursor pode ser sempre usada (SQL_CUR_USE_ODBC), usado somente se o driver não dá suporte a cursores roláveis (SQL_CUR_USE_IF_NEEDED) ou nunca foi usado (SQL_CUR_USE_DRIVER).  
  
2.  Chamadas **SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect** para se conectar à fonte de dados.  
  
3.  Chamadas **SQLSetStmtAttr** para especificar o tipo de cursor (SQL_ATTR_CURSOR_TYPE), a simultaneidade (SQL_ATTR_CONCURRENCY) e o tamanho do conjunto de linhas (SQL_ATTR_ROW_ARRAY_SIZE). A biblioteca de cursores dá suporte a cursores de somente avanço e estáticos. Cursores de somente avanço devem ser somente leitura, enquanto os cursores estáticos podem ser somente leitura ou podem usar o controle de simultaneidade otimista comparar valores.  
  
4.  Aloca um ou mais buffers de linhas e chamadas **SQLBindCol** uma ou mais vezes para associar esses buffers para colunas do conjunto de resultados.  
  
5.  Gera um resultado definido ao executar uma **selecione** instrução ou um procedimento, ou chamando uma função de catálogo. Se o aplicativo será executado instruções update posicionadas, ele deverá ser executado um **Selecione para atualizar** instrução para gerar o conjunto de resultados.  
  
6.  Chamadas **SQLFetch** ou **SQLFetchScroll** uma ou mais vezes para percorrer o conjunto de resultados.  
  
 O aplicativo pode alterar valores de dados em buffers do conjunto de linhas. Para atualizar os buffers de conjunto de linhas com dados de cache da biblioteca de cursor, um aplicativo chama **SQLFetchScroll** com o *FetchOrientation* argumento definido como SQL_FETCH_RELATIVE e  *FetchOffset* argumento definido como 0.  
  
 Para recuperar dados de uma coluna não associada, o aplicativo chama **SQLSetPos** para posicionar o cursor na linha desejada. Depois, ele chama **SQLGetData** para recuperar os dados.  
  
 Para determinar o número de linhas que foram recuperados da fonte de dados, o aplicativo chama **SQLRowCount**.
