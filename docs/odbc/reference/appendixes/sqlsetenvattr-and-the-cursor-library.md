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
ms.openlocfilehash: db1608415ae74bcaafd89f4afe01393cfb700379
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125563"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e a Biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetEnvAttr** com a biblioteca de cursores. Para obter informações gerais sobre **SQLSetEnvAttr**, consulte [SQLSetEnvAttr function](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 A biblioteca de cursores não é afetada pela configuração do atributo de ambiente SQL_ATTR_ODBC_VERSION, independentemente da versão do aplicativo ou da versão do driver.
