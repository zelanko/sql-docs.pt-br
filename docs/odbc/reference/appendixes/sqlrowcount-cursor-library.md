---
title: SQLRowCount (Biblioteca cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9fe597f54ecb4bc82439251e2228ac5fdc4ea3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300576"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLRowCount** na biblioteca do cursor. Para obter informações gerais sobre **o SQLRowCount,** consulte [SQLRowCount Function](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Quando um aplicativo chama **sqlrowcount** com a declaração associada ao cursor, a biblioteca do cursor retorna o número de linhas de dados que recuperou do driver.  
  
 Quando um aplicativo chama **o SQLRowCount** com a declaração associada a uma atualização posicionada ou à declaração de exclusão, a biblioteca do cursor retorna o número de linhas afetadas pela declaração.  
  
 Quando um aplicativo chama **SQLRowCount** após uma declaração **SELECT,** a biblioteca do cursor retorna -1.
