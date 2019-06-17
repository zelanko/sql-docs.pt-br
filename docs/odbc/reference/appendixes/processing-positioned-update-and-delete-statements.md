---
title: Processamento posicionado instruções Update e Delete | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d898fcc7d1b35230173afa0443219d59c54720ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057069"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Processar instruções de atualização e exclusão posicionadas
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 O suporta da biblioteca de cursor posicionado instruções update e delete, substituindo o **WHERE CURRENT OF** cláusula em tais instruções com um **onde** cláusula que enumera os valores armazenados em seu cache para cada coluna associada. A biblioteca de cursores passa recentemente construído **atualização** e **excluir** instruções para o driver para execução. Para instruções de atualização posicionada, a biblioteca de cursores, em seguida, atualiza seu cache entre os valores nos buffers de conjunto de linhas e define o valor correspondente na matriz de status de linha para SQL_ROW_UPDATED. Para instruções delete posicionadas, ele define o valor correspondente na matriz de status de linha para SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identifique uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md), mais adiante neste apêndice.  
  
 Posicionado update e delete instruções estão sujeitos às seguintes restrições:  
  
-   Posicionado update e delete instruções podem ser usadas apenas nos seguintes casos: quando um **selecionar** instrução gerou o conjunto de resultados; quando o **selecionar** instrução não continha uma junção, um  **União** cláusula, ou um **GROUP BY** cláusula; e quando todas as colunas que é usado um alias ou uma expressão na lista de seleção não foram vinculadas com **SQLBindCol**.  
  
-   Se um aplicativo prepara uma instrução de exclusão ou atualização posicionada, deverá fazê-lo depois que ele chamou **SQLFetch** ou **SQLFetchScroll**. Embora a biblioteca de cursores envia a instrução para o driver para a preparação, ele fecha a instrução e o executa diretamente quando o aplicativo chama **SQLExecute**.  
  
-   Se o driver dá suporte a apenas uma instrução ativa, as buscas do cursor biblioteca o restante do resultado definido e refetches, em seguida, o conjunto de linhas atual de seu cache antes de executar um posicionadas instrução update ou delete. Se o aplicativo chama uma função que retorna metadados em um conjunto de resultados (por exemplo, **SQLNumResultCols** ou **SQLDescribeCol**), a biblioteca de cursores retornará um erro.  
  
-   Se uma atualização posicionada ou uma instrução delete for executada em uma coluna de uma tabela que inclui uma coluna de carimbo de hora é atualizada automaticamente sempre que uma atualização é executada, todas as próximas atualização posicionada ou instruções delete falhará se a coluna de carimbo de hora associado. Isso ocorre porque o pesquisada update ou delete instrução que cria a biblioteca de cursores não identificará com precisão a linha a ser atualizada. O valor na instrução pesquisada para a coluna de carimbo de hora não corresponderá o valor atualizado automaticamente da coluna de carimbo de hora.
