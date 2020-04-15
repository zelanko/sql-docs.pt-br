---
title: Recuperando marcadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300066"
---
# <a name="retrieving-bookmarks"></a>Recuperar indicadores
Se o aplicativo usar marcadores, ele deve definir o atributo de declaração SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE antes de preparar ou executar a declaração. Isso é necessário porque construir e manter marcadores pode ser uma operação cara, por isso os marcadores devem ser habilitados apenas quando um aplicativo pode fazer bom uso deles.  
  
 Os marcadores são devolvidos como a coluna 0 do conjunto de resultados. Há três maneiras de um aplicativo recuperá-los:  
  
-   Vincule a coluna 0 do conjunto de resultados. **SQLFetch** ou **SQLFetchScroll** retorna os marcadores para cada linha no conjunto de linhas, juntamente com os dados de outras colunas vinculadas.  
  
-   Ligue para **SQLSetPos** para posicionar-se em uma linha no conjunto de linhas e, em seguida, chame **SQLGetData** para a coluna 0. Se um driver suportar marcadores, ele deve sempre suportar a capacidade de chamar **SQLGetData** para a coluna 0, mesmo que não permita que aplicativos chamem **SQLGetData** para outras colunas antes da última coluna vinculada.  
  
-   Ligue para **a SQLBulkOperations** com o argumento *Operação* definido para SQL_ADD e a coluna 0 vinculada. O cursor insere a linha e retorna o marcador para a linha no buffer bound.
