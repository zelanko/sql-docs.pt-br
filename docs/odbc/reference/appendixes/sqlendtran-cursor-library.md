---
title: SQLEndTran (biblioteca de Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf28f3e0073a9a3461f4c52636521ed60959a783
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLEndTran** função na biblioteca de cursor. Para obter informações gerais sobre **SQLEndTran**, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 A biblioteca de cursores não oferece suporte a transações e passa a chamadas para **SQLEndTran** diretamente para o driver. No entanto, a biblioteca de cursores dá suporte os comportamentos de cursor commit e rollback conforme retornado pela fonte de dados com os tipos de informações SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Para fontes de dados que preservam cursores em transações, as alterações serão revertidas na fonte de dados não serão revertidas no cache da biblioteca de cursor. Para fazer com que o cache corresponderem aos dados na fonte de dados, o aplicativo deve fechar e reabra o cursor.  
  
-   Para fontes de dados que fechar cursores em limites de transação, a biblioteca de cursores fecha os cursores e exclui os caches para todas as instruções sobre a conexão.  
  
-   Para fontes de dados que excluir instruções preparadas em limites de transação, o aplicativo deve reprepare todas as instruções preparadas na conexão antes de executar novamente a eles.
