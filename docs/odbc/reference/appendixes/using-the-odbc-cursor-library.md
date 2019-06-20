---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fe19efb2d39e875cdafec76f2c50164f3a66f03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735013"
---
# <a name="using-the-odbc-cursor-library"></a>Usar a biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para usar a biblioteca de cursores ODBC, um aplicativo:  
  
1.  Chamadas **SQLSetConnectAttr** com um *atributo* de SQL_ATTR_ODBC_CURSORS para especificar como a biblioteca de cursores deve ser usada com uma conexão específica. A biblioteca de cursores pode ser sempre usada (SQL_CUR_USE_ODBC), usada somente se o driver não oferece suporte a cursores roláveis (SQL_CUR_USE_IF_NEEDED) ou nunca utilizados (SQL_CUR_USE_DRIVER).  
  
2.  Chamadas **SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect** para se conectar à fonte de dados.  
  
3.  Chamadas **SQLSetStmtAttr** para especificar o tipo de cursor (SQL_ATTR_CURSOR_TYPE), a simultaneidade (SQL_ATTR_CONCURRENCY) e o tamanho do conjunto de linhas (SQL_ATTR_ROW_ARRAY_SIZE). A biblioteca de cursores dá suporte a cursores de somente avanço e estáticos. Cursores de somente avanço devem ser somente leitura, enquanto os cursores estáticos podem ser somente leitura ou podem usar a comparação de valores de controle de simultaneidade otimista.  
  
4.  Aloca um ou mais buffers de conjunto de linhas e chamadas **SQLBindCol** uma ou mais vezes para associar esses buffers para colunas do conjunto de resultados.  
  
5.  Gera um resultado definido ao executar uma **selecionar** instrução ou procedimento, ou chamando uma função de catálogo. Se o aplicativo executará instruções update posicionadas, ele deve executar uma **Selecione para atualizar** instrução para gerar o conjunto de resultados.  
  
6.  Chamadas **SQLFetch** ou **SQLFetchScroll** uma ou mais vezes para percorrer o conjunto de resultados.  
  
 O aplicativo pode alterar os valores de dados nos buffers de conjunto de linhas. Para atualizar os buffers de conjunto de linhas com dados do cache da biblioteca de cursor, um aplicativo chama **SQLFetchScroll** com o *FetchOrientation* argumento definido como SQL_FETCH_RELATIVE e o  *FetchOffset* argumento definido como 0.  
  
 Para recuperar dados de uma coluna não associada, o aplicativo chama **SQLSetPos** para posicionar o cursor na linha desejada. Em seguida, ele chama **SQLGetData** para recuperar os dados.  
  
 Para determinar o número de linhas que foram recuperados da fonte de dados, o aplicativo chama **SQLRowCount**.
