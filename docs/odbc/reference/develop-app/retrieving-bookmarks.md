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
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020568"
---
# <a name="retrieving-bookmarks"></a>Recuperar indicadores
Se o aplicativo usar indicadores, ele deverá definir o atributo SQL_ATTR_USE_BOOKMARKS Statement como SQL_UB_VARIABLE antes de preparar ou executar a instrução. Isso é necessário porque criar e manter indicadores pode ser uma operação cara, portanto, os indicadores devem ser habilitados somente quando um aplicativo puder fazer um bom uso deles.  
  
 Os indicadores são retornados como a coluna 0 do conjunto de resultados. Há três maneiras pelas quais um aplicativo pode recuperá-los:  
  
-   Associe a coluna 0 do conjunto de resultados. **SQLFetch** ou **SQLFetchScroll** retorna os indicadores para cada linha no conjunto de linhas junto com os dados para outras colunas associadas.  
  
-   Chame **SQLSetPos** para posicioná-lo em uma linha no conjunto de linhas e, em seguida, chame **SQLGetData** para a coluna 0. Se um driver oferecer suporte a indicadores, ele deverá sempre oferecer suporte à capacidade de chamar **SQLGetData** para a coluna 0, mesmo que não permita que os aplicativos chamem **SQLGetData** para outras colunas antes da última coluna associada.  
  
-   Chame **SQLBulkOperations** com o argumento de *operação* definido como SQL_ADD e a coluna 0 associada. O cursor insere a linha e retorna o indicador para a linha no buffer associado.
