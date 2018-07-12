---
title: Indicando linhas em ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb9f3284ab180ed05acc2a199c3b8cece8a1e40b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430695"
---
# <a name="bookmarking-rows-in-odbc"></a>Indicando linhas em ODBC
  Um indicador é um valor usado para identificar uma linha de dados. O significado do valor de indicador só é conhecido para o driver ou a fonte de dados. Por exemplo, ele poderá ser tão simples quanto um número de linha ou tão complexo quanto um endereço de disco. Em ODBC, o aplicativo solicita um indicador para uma linha específica, armazena-o e transmite-o novamente ao cursor para que retorne à linha.  
  
 Ao buscar linhas com [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md), um aplicativo pode usar um indicador como base para selecionar a linha inicial. Esta é uma forma de endereçamento absoluto porque não depende da posição atual do cursor. Para rolar para uma linha marcada com indicador, o aplicativo chama **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operação usa o indicador apontado pelo atributo da opção SQL_ATTR_FETCH_BOOKMARK_PTR. Retorna o conjunto de linhas que inicia com a linha identificada por esse indicador. Um aplicativo pode especificar um deslocamento para esta operação é o *FetchOffset* argumento da chamada para **SQLFetchScroll**. Quando um deslocamento é especificado, a primeira linha do conjunto de linhas retornado é determinada adicionando o número no argumento FetchOffset ao número da linha identificada pelo indicador. O driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client apenas dá suporte a indicadores em cursores estáticos e do conjunto de chaves. Se um cursor dinâmico for solicitado quando indicadores forem definidos, um cursor do conjunto de chaves será aberto no lugar.  
  
 Indicadores também podem ser usados com o **SQLBulkOperations** função para executar operações em um conjunto de linhas que iniciam no indicador.  
  
## <a name="see-also"></a>Consulte também  
 [Rolagem e busca de linhas](../native-client-ole-db-rowsets/fetching-rows.md)  
  
  
