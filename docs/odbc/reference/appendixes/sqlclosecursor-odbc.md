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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68123379"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLCloseCursor** na biblioteca de cursores. Para obter informações gerais sobre **SQLCloseCursor**, consulte [SQLCloseCursor function](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 A biblioteca de cursores não dá suporte à chamada de **SQLCloseCursor** sem um cursor aberto. Tentar isso retornará SQLSTATE 24000 (estado de cursor inválido). Chamar **SQLFreeStmt** com uma *opção* de SQL_CLOSE quando nenhum cursor está aberto é suportado pela biblioteca de cursores.
