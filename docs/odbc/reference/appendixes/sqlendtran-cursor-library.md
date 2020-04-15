---
title: SQLEndTran (Biblioteca Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2277a67cd5410ea3c2a5d5b03b16d4533ed6ee1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304759"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLEndTran** na biblioteca do cursor. Para obter informações gerais sobre **o SQLEndTran,** consulte [SQLEndTran Function](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 A biblioteca do cursor não suporta transações e passa chamadas para **o SQLEndTran** diretamente para o driver. No entanto, a biblioteca do cursor suporta os comportamentos de confirmação e reversão do cursor, conforme retornado pela fonte de dados com os tipos de informações SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Para fontes de dados que preservam cursores em transações, as alterações que são revertidas na fonte de dados não são revertidas no cache da biblioteca do cursor. Para fazer o cache corresponder aos dados na fonte de dados, o aplicativo deve fechar e reabrir o cursor.  
  
-   Para fontes de dados que fecham cursors nos limites da transação, a biblioteca do cursor fecha os cursores e exclui os caches de todas as declarações na conexão.  
  
-   Para fontes de dados que excluem declarações preparadas nos limites da transação, o aplicativo deve repreparar todas as declarações preparadas sobre a conexão antes de executá-las.
