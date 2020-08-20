---
description: SQLEndTran (Biblioteca de cursores)
title: SQLEndTran (biblioteca de cursores) | Microsoft Docs
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
ms.openlocfilehash: 25584f19a885580be24b2681ccd639de285fb4b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466028"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLEndTran** na biblioteca de cursores. Para obter informações gerais sobre **SQLEndTran**, consulte [SQLEndTran function](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 A biblioteca de cursores não oferece suporte a transações e passa chamadas para **SQLEndTran** diretamente para o driver. No entanto, a biblioteca de cursores oferece suporte aos comportamentos de confirmação e reversão do cursor, conforme retornado pela fonte de dados com os tipos de informações SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Para fontes de dados que preservam cursores entre transações, as alterações revertidas na fonte de dados não são revertidas no cache da biblioteca de cursores. Para fazer com que o cache corresponda aos dados na fonte de dados, o aplicativo deve fechar e reabrir o cursor.  
  
-   Para fontes de dados que fecham cursores em limites de transação, a biblioteca de cursores fecha os cursores e exclui os caches para todas as instruções na conexão.  
  
-   Para fontes de dados que excluem instruções preparadas em limites de transação, o aplicativo deve repreparar todas as instruções preparadas na conexão antes de executá-las novamente.
