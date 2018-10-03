---
title: SQLSetEnvAttr e a biblioteca de cursores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74e57f98b7d5e3e1508a960b342521ea5d315a3d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693484"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e a Biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetEnvAttr** função com a biblioteca de cursores. Para obter informações gerais sobre **SQLSetEnvAttr**, consulte [função SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 A biblioteca de cursores é afetada pela configuração do atributo ambiente SQL_ATTR_ODBC_VERSION, independentemente da versão do driver ou a versão do aplicativo.
