---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9eecd202a17a0a08e8607ebec0caaa31b7b3ca9c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199201"
---
# <a name="bookmarks-odbc"></a>Indicadores (ODBC)
Um indicador é um valor usado para identificar uma linha de dados. O significado do valor de indicador só é conhecido para o driver ou a fonte de dados. Por exemplo, ele poderá ser tão simples quanto um número de linha ou tão complexo quanto um endereço de disco. Os indicadores no ODBC são um pouco diferentes de indicadores em livros real. Em um livro real, o leitor coloca um indicador em uma página específica e, em seguida, procura por esse indicador retornar à página. Em ODBC, o aplicativo solicita um indicador para uma linha específica, armazena-o e transmite-o novamente ao cursor para que retorne à linha. Assim, os indicadores no ODBC são semelhantes a um leitor anotar um número de página, lembrá-la e, em seguida, verificando novamente a página.  
  
 Para determinar o suporte de um driver de indicadores, um aplicativo chama **SQLGetInfo** com a opção SQL_BOOKMARK_PERSISTENCE. Os bits nesse valor de descrevem o que os indicadores de operações sobrevivem, como se os indicadores são ainda são válidos depois que o cursor é fechado.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de indicador](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recuperando indicadores](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Rolando pelo indicador](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Atualizar, excluir ou buscar por indicador](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Comparando indicadores](../../../odbc/reference/develop-app/comparing-bookmarks.md)
