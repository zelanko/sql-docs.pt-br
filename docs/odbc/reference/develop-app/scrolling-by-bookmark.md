---
title: Rolar pelo indicador | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10ba29b2556b5c58fa47b44a31755cfbefc07214
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="scrolling-by-bookmark"></a>Rolar pelo indicador
Ao buscar linhas com **SQLFetchScroll**, um aplicativo pode usar um indicador como uma base para selecionar a linha inicial. Esta é uma forma de endereçamento absoluto porque não depende da posição atual do cursor. Para rolar até uma linha marcada, o aplicativo chama **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_BOOKMARK. Essa operação usa o indicador apontado pelo atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR. Retorna o conjunto de linhas que inicia com a linha identificada por esse indicador. Um aplicativo pode especificar um deslocamento para esta operação é o *FetchOffset* argumento da chamada para **SQLFetchScroll**. Quando um deslocamento for especificado, a primeira linha do conjunto de linhas retornado é determinada pela adição do número no *FetchOffset* argumento para o número da linha identificada pelo indicador. Esse uso do *FetchOffset* argumento não é suportado quando usado com o ODBC 2. *x* drivers; quando um aplicativo chama **SQLFetchScroll** em um ODBC 2. *x* driver com *FetchOrientation* definida como SQL_FETCH_BOOKMARK, o *FetchOffset* argumento deve ser definido como 0.
