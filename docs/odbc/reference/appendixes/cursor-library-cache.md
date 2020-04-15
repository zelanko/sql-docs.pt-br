---
title: Cache da Biblioteca cursor | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284686"
---
# <a name="cursor-library-cache"></a>Cache de biblioteca de cursores
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Para cada linha de dados no conjunto de resultados, a biblioteca do cursor armazena os dados de cada coluna vinculada, o comprimento dos dados em cada coluna vinculada e o status da linha. A biblioteca do cursor usa os valores no cache tanto para retornar através **do SQLFetch** e **sQLFetchScroll** e para construir instruções pesquisadas para operações posicionadas. Para obter mais informações, consulte [Construindo declarações pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Dados de coluna](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Comprimento dos dados da coluna](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Status da linha](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Local do cache](../../../odbc/reference/appendixes/location-of-cache.md)
