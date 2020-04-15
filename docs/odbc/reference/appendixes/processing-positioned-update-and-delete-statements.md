---
title: Processamento de instruções de atualização posicionada e exclusão | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b3f20da018bcd4e28e8ffca097fb5a4373d7f42
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308017"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Processar instruções de atualização e exclusão posicionadas
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor suporta instruções de atualização posicionadas e exclusão, substituindo a cláusula **WHERE CURRENT OF** em tais instruções por uma cláusula **WHERE** que enumera os valores armazenados em seu cache para cada coluna vinculada. A biblioteca do cursor passa as instruções atualizadas **UPDATE** e **DELETE** para o driver para execução. Para instruções de atualização posicionadas, a biblioteca do cursor atualiza seu cache a partir dos valores nos buffers de conjunto de linhas e define o valor correspondente na matriz de status da linha para SQL_ROW_UPDATED. Para as instruções de exclusão posicionadas, ele define o valor correspondente na matriz de status da linha para SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  A cláusula **WHERE** construída pela biblioteca cursor para identificar a linha atual pode não identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [Construindo Declarações Pesquisadas,](../../../odbc/reference/appendixes/constructing-searched-statements.md)mais tarde neste apêndice.  
  
 As instruções de atualização e exclusão posicionadas estão sujeitas às seguintes restrições:  
  
-   As instruções de atualização e exclusão posicionadas só podem ser usadas nos seguintes casos: quando uma instrução **SELECT** gerou o conjunto de resultados; quando a declaração **SELECT** não continha uma adesão, uma cláusula **da UNIÃO** ou uma cláusula **GROUP BY;** e quando quaisquer colunas que usavam um alias ou expressão na lista de seleção não estavam vinculadas ao **SQLBindCol**.  
  
-   Se um aplicativo prepara uma declaração de atualização posicionada ou exclusão, ele deve fazê-lo depois de ter chamado **SQLFetch** ou **SQLFetchScroll**. Embora a biblioteca do cursor envie a declaração ao driver para preparação, ela fecha a declaração e a executa diretamente quando o aplicativo chama **SQLExecute**.  
  
-   Se o driver suportar apenas uma declaração ativa, a biblioteca do cursor busca o resto do conjunto de resultados e, em seguida, rebusca o conjunto de linhas atual de seu cache antes de executar uma declaração de atualização posicionada ou excluir. Se o aplicativo então chamar uma função que retorna metadados em um conjunto de resultados (por exemplo, **SQLNumResultCols** ou **SQLDescribeCol),** a biblioteca do cursor retorna um erro.  
  
-   Se uma instrução de atualização ou exclusão posicionada for realizada em uma coluna de uma tabela que inclua uma coluna de carimbo de data e hora que é atualizada automaticamente toda vez que uma atualização for realizada, todas as instruções de atualização posicionadas subseqüentes ou exclusão falharão se a coluna de carimbo de tempo estiver vinculada. Isso ocorre porque a declaração de atualização ou exclusão pesquisada que a biblioteca de cursor cria não identificará com precisão a linha a ser atualizada. O valor na declaração pesquisada para a coluna carimbo de tempo não corresponderá ao valor atualizado automaticamente da coluna carimbo de data e hora.
