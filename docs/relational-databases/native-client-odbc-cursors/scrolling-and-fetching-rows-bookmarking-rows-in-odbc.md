---
title: Linhas de indicador no ODBC | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88541982e6d79fb1f81f942f58114d9ba25f692d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998973"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>Rolagem e busca de linhas – Marcação de linhas em ODBC
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Um indicador é um valor usado para identificar uma linha de dados. O significado do valor de indicador só é conhecido para o driver ou a fonte de dados. Por exemplo, ele poderá ser tão simples quanto um número de linha ou tão complexo quanto um endereço de disco. Em ODBC, o aplicativo solicita um indicador para uma linha específica, armazena-o e transmite-o novamente ao cursor para que retorne à linha.  
  
 Ao buscar linhas com [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md), um aplicativo pode usar um indicador como base para selecionar a linha inicial. Esta é uma forma de endereçamento absoluto porque não depende da posição atual do cursor. Para rolar para uma linha com indicador, o aplicativo chama **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK. Esta operação usa o indicador apontado pelo atributo da opção SQL_ATTR_FETCH_BOOKMARK_PTR. Retorna o conjunto de linhas que inicia com a linha identificada por esse indicador. Um aplicativo pode especificar um deslocamento para essa operação no argumento *FetchOffset* da chamada para **SQLFetchScroll**. Quando um deslocamento é especificado, a primeira linha do conjunto de linhas retornado é determinada adicionando o número no argumento FetchOffset ao número da linha identificada pelo indicador. O driver ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client apenas dá suporte a indicadores em cursores estáticos e do conjunto de chaves. Se um cursor dinâmico for solicitado quando indicadores forem definidos, um cursor do conjunto de chaves será aberto no lugar.  
  
 Os indicadores também podem ser usados com a função **SQLBulkOperations** para executar operações em um conjunto de linhas, começando no indicador.  
  
## <a name="see-also"></a>Consulte Também  
 [Rolando e buscando linhas](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
