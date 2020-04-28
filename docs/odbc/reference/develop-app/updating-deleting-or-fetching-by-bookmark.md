---
title: Atualizando, excluindo ou buscando por indicador | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286146"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Atualizar, excluir ou buscar por indicador
Os indicadores podem ser usados para identificar os dados a serem atualizados no conjunto de resultados, excluídos do conjunto de resultados ou obtidos do conjunto de resultados para os buffers de conjunto de linhas. Essas operações são executadas por uma chamada para **SQLBulkOperations** com um argumento de *opção* de SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK ou SQL_FETCH_BY_BOOKMARK. Os indicadores usados nessas operações são armazenados na coluna 0 dos buffers de conjunto de linhas. Ao atualizar por indicador, os dados dos quais as colunas do conjunto de resultados são atualizadas são recuperados dos buffers de conjunto de linhas. Para obter mais informações, consulte [atualizando dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
