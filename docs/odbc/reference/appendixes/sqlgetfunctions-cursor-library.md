---
title: SQLGetFunctions (Biblioteca cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f993a08aae1656b8d373911299e75852de855419
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307817"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLGetFunctions** na biblioteca do cursor. Para obter informações gerais sobre **SQLGetFunctions,** consulte [SQLGetFunctions Functions .](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 Quando você chama **SQLGetFunctions,** a biblioteca do cursor retorna que suporta **SQLExtendedFetch,** **SQLFetchScroll,** **SQLSetPos**e **SQLSetScrollOptions,** além das funções suportadas pelo driver.
