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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296296"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLCloseCursor** na biblioteca do cursor. Para obter informações gerais sobre **o SQLCloseCursor,** consulte [SQLCloseCursor Function](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 A biblioteca do cursor não suporta chamar **SQLCloseCursor** sem um cursor aberto. A tentativa de isso retornará SQLSTATE 24000 (estado de cursor inválido). Chamar **sqlFreeStmt** com uma *opção* de SQL_CLOSE quando nenhum cursor está aberto é suportado pela biblioteca do cursor.
