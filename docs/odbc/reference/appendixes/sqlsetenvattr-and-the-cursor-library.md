---
title: SQLSetEnvAttr e a Biblioteca Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42d6804bf8a3544de44c03266ce28712e1b04d90
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300516"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e a Biblioteca de cursores
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetEnvAttr** com a biblioteca do cursor. Para obter informações gerais sobre **sqlsetenvAttr**, consulte [SQLSetEnvAttr Function](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 A biblioteca do cursor não é afetada pela configuração do atributo ambiente SQL_ATTR_ODBC_VERSION, independentemente da versão do aplicativo ou da versão do driver.
