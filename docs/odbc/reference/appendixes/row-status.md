---
title: Status de linha | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c30e5f98a4b55c028087618d99efbf5f452d2162
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="row-status"></a>Status de linha
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 A biblioteca de cursores cria um buffer em cache para o status de linha. A biblioteca de cursores recupera os valores para a matriz de status de linha (especificado com o atributo de instrução SQL_ATTR_ROW_STATUS_PTR) nesse buffer. Para cada linha, a biblioteca de cursores define esse buffer:  
  
-   SQL_ROW_DELETED quando executa um posicionadas exclusão da instrução na linha.  
  
-   SQL_ROW_ERROR quando encontra um erro ao recuperar a linha da fonte de dados com **SQLFetch**.  
  
-   SQL_ROW_SUCCESS quando ele busca com êxito a linha da fonte de dados com **SQLFetch**.  
  
-   SQL_ROW_UPDATED quando ele executa uma instrução de atualização posicionada na linha.
