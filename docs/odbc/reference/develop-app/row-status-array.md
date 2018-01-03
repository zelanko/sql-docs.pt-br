---
title: Matriz de Status de linha | Microsoft Docs
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
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 35f61dfb550c54c47e821476687320125b60b7e1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="row-status-array"></a>Matriz de Status de linha
Além dos dados, **SQLFetch** e **SQLFetchScroll** pode retornar uma matriz que fornece o status de cada linha no conjunto de linhas. Esta matriz é especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR. Esta matriz é alocada pelo aplicativo e deve ter elementos são especificadas pelo atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE. Os valores na matriz são definidos **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, e **SQLSetPos.** Os valores descrevem o status da linha e se o status foi alterado desde a última busca.  
  
|Valor de matriz de status de linha|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi obtida com êxito e não alterados desde a última busca.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi obtida com êxito e não alterados desde a última busca. No entanto, um aviso sobre a linha foi retornado.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED|A linha foi obtida com êxito e tiver sido atualizada desde a última busca. Se a linha é novamente buscada ou atualizada por **SQLSetPos**, seu status é alterado para o novo status.<br /><br /> Alguns drivers não podem detectar alterações aos dados e, portanto, não é possível retornar esse valor. Para determinar se um driver pode detectar as atualizações para linhas refetched, um aplicativo chama **SQLGetInfo** com a opção SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|A linha foi excluída desde a última busca.|  
|SQL_ROW_ADDED|A linha foi inserida por **SQLBulkOperations**. Se a linha será buscada novamente ou é atualizada por **SQLSetPos**, seu status é SQL_ROW_SUCCESS.<br /><br /> Esse valor não está definido por **SQLFetch** ou **SQLFetchScroll**.|  
|SQL_ROW_NOROW|O conjunto de linhas sobrepostos final do conjunto de resultados, e nenhuma linha foi retornada que correspondeu a esse elemento da matriz de status de linha.|
