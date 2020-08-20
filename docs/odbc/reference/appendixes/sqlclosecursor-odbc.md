---
description: SQLCloseCursor_ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91ce573a48602ad6dce4f0cb0759c2c8dddd3aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466048"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLCloseCursor** na biblioteca de cursores. Para obter informações gerais sobre **SQLCloseCursor**, consulte [SQLCloseCursor function](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 A biblioteca de cursores não dá suporte à chamada de **SQLCloseCursor** sem um cursor aberto. Tentar isso retornará SQLSTATE 24000 (estado de cursor inválido). Chamar **SQLFreeStmt** com uma *opção* de SQL_CLOSE quando nenhum cursor está aberto é suportado pela biblioteca de cursores.
