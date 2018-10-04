---
title: Atualizar, excluir ou buscar por indicador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5af3cad39739c3b85a0c6298d682d8e75a5918d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765794"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>Atualizar, excluir ou buscar por indicador
Indicadores podem ser usados para identificar os dados a serem atualizados no conjunto de resultados, excluído do resultado definido ou buscadas no conjunto de resultados para os buffers de conjunto de linhas. Essas operações são executadas por uma chamada para **SQLBulkOperations** com um *opção* argumento SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK ou SQL_FETCH_BY_BOOKMARK. Os indicadores usados nessas operações são armazenados na coluna 0 dos buffers de linhas. Ao atualizar pelo indicador, os dados que colunas do conjunto de resultados são atualizados para é recuperada dos buffers de conjunto de linhas. Para obter mais informações, consulte [atualizando dados com SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).
