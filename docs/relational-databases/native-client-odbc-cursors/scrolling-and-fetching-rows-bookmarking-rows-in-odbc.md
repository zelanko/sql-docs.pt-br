---
title: Indicando linhas em ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d58ce5236a2d74e1749e88f0bffa9ca86f974733
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803707"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>Rolagem e busca de linhas – Marcação de linhas em ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um indicador é um valor usado para identificar uma linha de dados. O significado do valor de indicador só é conhecido para o driver ou a fonte de dados. Por exemplo, ele poderá ser tão simples quanto um número de linha ou tão complexo quanto um endereço de disco. Em ODBC, o aplicativo solicita um indicador para uma linha específica, armazena-o e transmite-o novamente ao cursor para que retorne à linha.  
  
 Ao buscar linhas com [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md), um aplicativo pode usar um indicador como base para selecionar a linha inicial. Esta é uma forma de endereçamento absoluto porque não depende da posição atual do cursor. Para rolar para uma linha marcada com indicador, o aplicativo chama **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operação usa o indicador apontado pelo atributo da opção SQL_ATTR_FETCH_BOOKMARK_PTR. Retorna o conjunto de linhas que inicia com a linha identificada por esse indicador. Um aplicativo pode especificar um deslocamento para esta operação é o *FetchOffset* argumento da chamada para **SQLFetchScroll**. Quando um deslocamento é especificado, a primeira linha do conjunto de linhas retornado é determinada adicionando o número no argumento FetchOffset ao número da linha identificada pelo indicador. O driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client apenas dá suporte a indicadores em cursores estáticos e do conjunto de chaves. Se um cursor dinâmico for solicitado quando indicadores forem definidos, um cursor do conjunto de chaves será aberto no lugar.  
  
 Indicadores também podem ser usados com o **SQLBulkOperations** função para executar operações em um conjunto de linhas que iniciam no indicador.  
  
## <a name="see-also"></a>Consulte também  
 [Rolagem e busca de linhas](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
