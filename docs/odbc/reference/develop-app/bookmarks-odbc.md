---
description: Indicadores (ODBC)
title: Indicadores (ODBC) | Microsoft Docs
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
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f162fc317f2651549a1a2e80af03c9942dc64bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461608"
---
# <a name="bookmarks-odbc"></a>Indicadores (ODBC)
Um indicador é um valor usado para identificar uma linha de dados. O significado do valor de indicador só é conhecido para o driver ou a fonte de dados. Por exemplo, ele poderá ser tão simples quanto um número de linha ou tão complexo quanto um endereço de disco. Os indicadores no ODBC são um pouco diferentes dos indicadores em livros reais. Em um livro real, o leitor coloca um indicador em uma página específica e, em seguida, procura esse indicador para retornar à página. Em ODBC, o aplicativo solicita um indicador para uma linha específica, armazena-o e transmite-o novamente ao cursor para que retorne à linha. Assim, os indicadores no ODBC são semelhantes a um leitor que escreve um número de página, lembra-o e, em seguida, pesquisa a página novamente.  
  
 Para determinar o suporte de indicadores de um driver, um aplicativo chama **SQLGetInfo** com a opção SQL_BOOKMARK_PERSISTENCE. Os bits nesse valor descrevem quais indicadores de operações sobrevivem, como se os indicadores ainda são válidos depois que o cursor é fechado.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de indicador](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recuperar indicadores](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Rolar pelo indicador](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Atualizar, excluir ou buscar por indicador](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Comparar indicadores](../../../odbc/reference/develop-app/comparing-bookmarks.md)
