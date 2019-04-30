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
manager: craigg
ms.openlocfilehash: 827f7195c5d4eb4f67cb3298b75519a5583053d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199505"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLCloseCursor** função na biblioteca de cursor. Para obter informações gerais sobre **SQLCloseCursor**, consulte [função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 A biblioteca de cursores não oferece suporte a chamar **SQLCloseCursor** sem um cursor aberto. Tentar isso retornará SQLSTATE 24000 (estado de cursor inválido). Chamando **SQLFreeStmt** com um *opção* de SQL_CLOSE quando nenhum cursor é aberto dá suporte a biblioteca de cursores.
