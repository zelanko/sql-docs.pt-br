---
description: Processar instruções de atualização e exclusão posicionadas
title: Processando instruções UPDATE e DELETE posicionadas | Microsoft Docs
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
ms.openlocfilehash: f11e5acd8afe46397126ddb4c1d4127eb99fc67a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483199"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Processar instruções de atualização e exclusão posicionadas
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 A biblioteca de cursores dá suporte a instruções UPDATE e DELETE posicionadas substituindo a cláusula **Where Current of** em tais instruções por uma cláusula **Where** que enumera os valores armazenados em seu cache para cada coluna associada. A biblioteca de cursores passa as instruções **Update** e **delete** recém-criadas para o driver para execução. Para instruções UPDATE posicionadas, a biblioteca de cursores atualiza seu cache dos valores nos buffers de conjunto de linhas e define o valor correspondente na matriz de status de linha como SQL_ROW_UPDATED. Para instruções DELETE posicionadas, ele define o valor correspondente na matriz de status de linha como SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  A cláusula **Where** construída pela biblioteca de cursores para identificar a linha atual pode falhar ao identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md), posteriormente neste apêndice.  
  
 As instruções UPDATE e DELETE posicionadas estão sujeitas às seguintes restrições:  
  
-   As instruções UPDATE e DELETE posicionadas só podem ser usadas nos seguintes casos: quando uma instrução **Select** gerou o conjunto de resultados; Quando a instrução **Select** não continha uma junção, uma cláusula **Union** ou uma cláusula **Group by** ; e quando qualquer coluna que usou um alias ou uma expressão na lista de seleção não foi associada a **SQLBindCol**.  
  
-   Se um aplicativo prepara uma instrução UPDATE ou DELETE posicionada, ele deve fazer isso depois de ter chamado **SQLFetch** ou **SQLFetchScroll**. Embora a biblioteca de cursores envie a instrução para o driver para preparação, ela fecha a instrução e a executa diretamente quando o aplicativo chama **SQLExecute**.  
  
-   Se o driver oferecer suporte a apenas uma instrução ativa, a biblioteca de cursores buscará o restante do conjunto de resultados e, em seguida, buscará novamente o conjunto de linhas atual de seu cache antes de executar uma instrução UPDATE ou DELETE posicionada. Se o aplicativo chamar uma função que retorna metadados em um conjunto de resultados (por exemplo, **SQLNumResultCols** ou **SQLDescribeCol**), a biblioteca de cursores retornará um erro.  
  
-   Se uma instrução UPDATE ou DELETE posicionada for executada em uma coluna de uma tabela que inclui uma coluna timestamp que é automaticamente atualizada toda vez que uma atualização for executada, todas as instruções UPDATE ou DELETE posicionadas subsequentes falharão se a coluna timestamp estiver associada. Isso ocorre porque a instrução UPDATE ou DELETE pesquisada criada pela biblioteca de cursores não identificará com precisão a linha a ser atualizada. O valor na instrução pesquisada para a coluna timestamp não corresponderá ao valor atualizado automaticamente da coluna timestamp.
