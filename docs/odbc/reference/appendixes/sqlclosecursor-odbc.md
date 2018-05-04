---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6477530573cc6fccd173e1cb1fbed7c59141a4e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLCloseCursor** função na biblioteca de cursor. Para obter informações gerais sobre **SQLCloseCursor**, consulte [função SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 A biblioteca de cursores não suporta chamada **SQLCloseCursor** sem um cursor aberto. Tentativa isso retornará SQLSTATE 24000 (estado de cursor inválido). Chamando **SQLFreeStmt** com um *opção* de SQL_CLOSE quando nenhum cursor é aberto é suportada pela biblioteca de cursores.
