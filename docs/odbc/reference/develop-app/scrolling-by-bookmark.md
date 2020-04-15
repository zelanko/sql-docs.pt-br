---
title: Rolagem por Marcador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 454e29abdf848fdf4f4eaae090e7cc326f0048df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304187"
---
# <a name="scrolling-by-bookmark"></a>Rolar pelo indicador
Ao buscar linhas com **SQLFetchScroll,** um aplicativo pode usar um marcador como base para selecionar a linha inicial. Esta é uma forma de endereçamento absoluto porque não depende da posição atual do cursor. Para rolar para uma linha marcada, o aplicativo chama **SQLFetchScroll** com uma Orientação de *SQL_FETCH_BOOKMARK.* Esta operação usa o marcador apontado pelo atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR. Retorna o conjunto de linhas que inicia com a linha identificada por esse indicador. Um aplicativo pode especificar uma compensação para esta operação no argumento *FetchOffset* da chamada para **SQLFetchScroll**. Quando um deslocamento é especificado, a primeira linha do conjunto de linhas retornada é determinada adicionando o número no argumento *FetchOffset* ao número da linha identificada pelo marcador. Este uso do argumento *FetchOffset* não é suportado quando usado com ODBC 2. *x* drivers; quando um aplicativo chama **SQLFetchScroll** em um ODBC 2. *x* driver com *FetchOrientation* definido para SQL_FETCH_BOOKMARK, o argumento *FetchOffset* deve ser definido como 0.
