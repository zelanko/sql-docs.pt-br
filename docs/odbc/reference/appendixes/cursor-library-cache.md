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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95a8e01b42f8bdc2036457b5c8a9e0e4088c16fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821054"
---
# <a name="cursor-library-cache"></a>Cache de biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Para cada linha de dados no conjunto de resultados, a biblioteca de cursores armazena em cache os dados para cada coluna associada, o comprimento dos dados em cada coluna associada e o status da linha. A biblioteca de cursores usa os valores no cache para retornar por meio **SQLFetch** e **SQLFetchScroll** e para construir instruções pesquisadas para operações posicionadas. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Dados de coluna](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Comprimento dos dados da coluna](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Status da linha](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Local do cache](../../../odbc/reference/appendixes/location-of-cache.md)
