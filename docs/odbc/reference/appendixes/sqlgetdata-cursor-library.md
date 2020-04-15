---
title: SQLGetData (Biblioteca cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307837"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLGetData** na biblioteca do cursor. Para obter informações gerais sobre **o SQLGetData,** consulte [SQLGetData Function](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 A biblioteca do cursor implementa **o SQLGetData** construindo primeiro uma declaração **SELECT** com uma cláusula **WHERE** que enumera os valores armazenados em seu cache para cada coluna vinculada na linha atual. Em seguida, executa a declaração **SELECT** para reselecionar a linha e chama **SQLGetData** no driver para recuperar os dados da fonte de dados (em oposição ao cache).  
  
> [!CAUTION]  
>  A cláusula **WHERE** construída pela biblioteca cursor para identificar a linha atual pode não identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [Construindo declarações pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Se o atributo de declaração SQL_ATTR_USE_BOOKMARKS estiver definido como SQL_UB_VARIABLE, **o SQLGetData** poderá ser chamado na coluna 0 para retornar os dados do marcador.  
  
 As chamadas para **SQLGetData** estão sujeitas às seguintes restrições:  
  
-   **O SQLGetData** não pode ser chamado para cursores somente para avanços.  
  
-   **SQLGetData** só pode ser chamado quando as seguintes condições forem atendidas: uma declaração **SELECT** gerou o conjunto de resultados; a declaração **SELECT** não continha uma adesão, uma cláusula **da UNIÃO** ou uma cláusula **GROUP BY;** e quaisquer colunas que usassem um alias ou expressão na lista de seleção não estavam vinculadas ao **SQLBindCol**.  
  
-   Se o driver suportar apenas uma declaração ativa, a biblioteca do cursor buscará o resto do conjunto de resultados antes de executar a declaração **SELECT** e chamar **SQLGetData**.
