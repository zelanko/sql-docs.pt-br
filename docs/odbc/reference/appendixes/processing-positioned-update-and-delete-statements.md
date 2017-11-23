---
title: "Processamento posicionado instruções Update e Delete | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9061ad8221537eaa00eb40fab56fa10d3357198d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="processing-positioned-update-and-delete-statements"></a>Processamento posicionado instruções Update e Delete
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 O suporte de biblioteca de cursor posicionado instruções update e delete, substituindo o **WHERE CURRENT OF** cláusula em tais instruções com um **onde** cláusula que enumera os valores armazenados no cache para cada coluna associada. A biblioteca de cursores passa recentemente construído **atualização** e **excluir** instruções para o driver para execução. Para instruções de atualização posicionada, a biblioteca de cursores, em seguida, atualiza o cache dos valores nos buffers de linhas e define o valor correspondente na matriz de status de linha para SQL_ROW_UPDATED. Para instruções delete posicionada, ele define o valor correspondente na matriz de status de linha para SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisados](../../../odbc/reference/appendixes/constructing-searched-statements.md), mais adiante neste apêndice.  
  
 Posicionado update e delete instruções estão sujeitas às seguintes restrições:  
  
-   Posicionado update e delete instruções podem ser usadas apenas nos seguintes casos: quando um **selecione** instrução gerou o conjunto de resultados; quando o **selecione** instrução não continha uma junção, um  **União** cláusula, ou um **GROUP BY** cláusula; e quando as colunas que é usado um alias ou uma expressão na lista de seleção não foram vinculadas com **SQLBindCol**.  
  
-   Se um aplicativo prepara uma atualização posicionada ou uma instrução delete, ele deve fazer isso depois que ela é chamada de **SQLFetch** ou **SQLFetchScroll**. Embora a biblioteca de cursores envia a instrução para o driver para preparação, ele fecha a instrução e executa-o diretamente quando o aplicativo chama **SQLExecute**.  
  
-   Se o driver oferece suporte a apenas uma instrução ativa, buscas de biblioteca de cursor o restante do resultado definido e refetches, em seguida, o conjunto de linhas atual de seu cache antes de executar um posicionadas instrução update ou delete. Se o aplicativo chama uma função que retorna metadados em um conjunto de resultados (por exemplo, **SQLNumResultCols** ou **SQLDescribeCol**), a biblioteca de cursores retornará um erro.  
  
-   Se uma atualização posicionada ou uma instrução delete for executada em uma coluna de uma tabela que inclui uma coluna de carimbo de hora que é atualizada automaticamente sempre que uma atualização é executada, todas as demais atualização posicionada ou instruções delete irá falhar se a coluna de carimbo de hora associado. Isso ocorre porque pesquisado update ou delete instrução que cria a biblioteca de cursores não identifica com precisão a linha a ser atualizada. O valor na instrução pesquisada para a coluna de carimbo de hora não corresponderá o valor atualizado automaticamente da coluna de carimbo de hora.
