---
title: Recuperando indicadores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d7d4bd52a5f6e5b03a084cef4402e0a9044f97d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777612"
---
# <a name="retrieving-bookmarks"></a>Recuperar indicadores
Se o aplicativo irá usar indicadores, ele deve definir o atributo de instrução de SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE antes de preparar ou executar a instrução. Isso é necessário porque a criação e manutenção de indicadores podem ser uma operação cara, portanto, indicadores devem ser habilitados apenas quando um aplicativo pode ter uma boa usá-los.  
  
 Indicadores são retornados como a coluna 0 do conjunto de resultados. Há três maneiras de que um aplicativo pode recuperá-los:  
  
-   Associe a coluna 0 do conjunto de resultados. **SQLFetch** ou **SQLFetchScroll** retorna os indicadores para cada linha no conjunto de linhas, juntamente com os dados para outros associada colunas.  
  
-   Chame **SQLSetPos** para posicionar a uma linha no conjunto de linhas e, em seguida, chame **SQLGetData** para a coluna 0. Se um driver dá suporte a indicadores, ela sempre deverá dar suporte a capacidade de chamar **SQLGetData** para a coluna 0, mesmo se ele não permite que aplicativos chamem **SQLGetData** para outras colunas antes do último limite coluna.  
  
-   Chame **SQLBulkOperations** com o *operação* argumento definido como SQL_ADD e a coluna 0 associado. O cursor insere a linha e retorna o indicador da linha no buffer associado.
