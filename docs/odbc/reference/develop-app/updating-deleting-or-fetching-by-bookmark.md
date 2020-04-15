---
title: Atualização, exclusão ou busca por Marcador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e94a98bb577ef906afbb04539761fd07d15f772
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286146"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Atualizar, excluir ou buscar por indicador
Marcadores podem ser usados para identificar dados a serem atualizados no conjunto de resultados, excluídos do conjunto de resultados ou obtidos do conjunto de resultados para os buffers de conjunto de linhas. Essas operações são realizadas por uma chamada para **SQLBulkOperations** com um argumento *option* de SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK ou SQL_FETCH_BY_BOOKMARK. Os marcadores usados nessas operações são armazenados na coluna 0 dos buffers de conjunto de linhas. Ao atualizar por marcador, os dados para os que as colunas de conjunto de resultados são atualizados são recuperados dos buffers do conjunto de linhas. Para obter mais informações, consulte [Atualizando dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
