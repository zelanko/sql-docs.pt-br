---
title: Cache de biblioteca de cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5686bf0c3e261b1df947c02e2edaa419da498ecb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284686"
---
# <a name="cursor-library-cache"></a>Cache de biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para cada linha de dados no conjunto de resultados, a biblioteca de cursores armazena em cache os dados para cada coluna associada, o comprimento dos dados em cada coluna associada e o status da linha. A biblioteca de cursores usa os valores no cache para retornar por **SQLFetch** e **SQLFetchScroll** e para construir instruções pesquisadas para operações posicionadas. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Dados de coluna](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Comprimento dos dados da coluna](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Status da linha](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Local do cache](../../../odbc/reference/appendixes/location-of-cache.md)
