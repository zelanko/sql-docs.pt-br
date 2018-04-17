---
title: Recuperando indicadores | Microsoft Docs
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
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d31e012efba212b1acbac0d4127459147508fd1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="retrieving-bookmarks"></a>Recuperando indicadores
Se o aplicativo usar indicadores, ele deve definir o atributo de instrução de SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE antes de preparar ou executar a instrução. Isso é necessário porque a criação e manutenção de indicadores podem ser uma operação dispendiosa, portanto, indicadores devem ser habilitados somente quando um aplicativo pode ter uma boa utilizá-las.  
  
 Indicadores são retornados como coluna 0 do conjunto de resultados. Há três maneiras de que um aplicativo pode recuperá-las:  
  
-   Associe a coluna 0 do conjunto de resultados. **SQLFetch** ou **SQLFetchScroll** retorna os indicadores para cada linha no conjunto de linhas com os dados para outros associadas a colunas.  
  
-   Chamar **SQLSetPos** para posicionar uma linha no conjunto de linhas e, em seguida, chamar **SQLGetData** para a coluna 0. Se um driver dá suporte a indicadores, ele sempre deve oferecer suporte a capacidade de chamar **SQLGetData** para a coluna 0, mesmo se ele não permite que aplicativos chamar **SQLGetData** para outras colunas antes do último limite coluna.  
  
-   Chamar **SQLBulkOperations** com o *operação* argumento definido como SQL_ADD e a coluna 0 associado. O cursor insere a linha e retorna o indicador da linha no buffer associado.
