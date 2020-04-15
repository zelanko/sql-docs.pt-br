---
title: Marcadores (ODBC) | Microsoft Docs
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
ms.openlocfilehash: e8273c82b918024417e613ea44a2d26bafaf7d76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306317"
---
# <a name="bookmarks-odbc"></a>Indicadores (ODBC)
Um indicador é um valor usado para identificar uma linha de dados. O significado do valor de indicador só é conhecido para o driver ou a fonte de dados. Por exemplo, ele poderá ser tão simples quanto um número de linha ou tão complexo quanto um endereço de disco. Marcadores na ODBC são um pouco diferentes dos marcadores em livros reais. Em um livro real, o leitor coloca um marcador em uma página específica e, em seguida, procura que o marcador retorne à página. Em ODBC, o aplicativo solicita um indicador para uma linha específica, armazena-o e transmite-o novamente ao cursor para que retorne à linha. Assim, os marcadores no ODBC são semelhantes a um leitor escrevendo um número de página, lembrando-o e, em seguida, olhando a página novamente.  
  
 Para determinar o suporte de um driver a marcadores, um aplicativo chama **sqlGetInfo** com a opção SQL_BOOKMARK_PERSISTENCE. Os bits neste valor descrevem quais as operações que sobrevivem, como se os marcadores ainda são válidos após o cursor ser fechado.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de indicador](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [Recuperar indicadores](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [Rolar pelo indicador](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [Atualizar, excluir ou buscar por indicador](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [Comparar indicadores](../../../odbc/reference/develop-app/comparing-bookmarks.md)
