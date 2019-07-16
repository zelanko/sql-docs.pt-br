---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4d0f88d2d9eaba7d95ba887ffbe11e728320b17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123379"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLCloseCursor** função na biblioteca de cursor. Para obter informações gerais sobre **SQLCloseCursor**, consulte [função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 A biblioteca de cursores não oferece suporte a chamar **SQLCloseCursor** sem um cursor aberto. Tentar isso retornará SQLSTATE 24000 (estado de cursor inválido). Chamando **SQLFreeStmt** com um *opção* de SQL_CLOSE quando nenhum cursor é aberto dá suporte a biblioteca de cursores.
