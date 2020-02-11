---
title: SQLGetData (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5962882de08712dcff75790de7c58d69f965a3bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086380"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLGetData** na biblioteca de cursores. Para obter informações gerais sobre **SQLGetData**, consulte [SQLGetData function](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 A biblioteca de cursores implementa o **SQLGetData** primeiro construindo uma instrução **Select** com uma cláusula **Where** que enumera os valores armazenados em seu cache para cada coluna associada na linha atual. Em seguida, ele executa a instrução **Select** para selecionar novamente a linha e chama **SQLGetData** no driver para recuperar os dados da fonte de dados (em oposição ao cache).  
  
> [!CAUTION]  
>  A cláusula **Where** construída pela biblioteca de cursores para identificar a linha atual pode falhar ao identificar quaisquer linhas, identificar uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Se o atributo da instrução SQL_ATTR_USE_BOOKMARKS for definido como SQL_UB_VARIABLE, **SQLGetData** poderá ser chamado na coluna 0 para retornar os dados do indicador.  
  
 Chamadas para **SQLGetData** estão sujeitas às seguintes restrições:  
  
-   **SQLGetData** não pode ser chamado para cursores de somente avanço.  
  
-   **SQLGetData** pode ser chamado somente quando as seguintes condições são atendidas: uma instrução **Select** gerou o conjunto de resultados; a instrução **Select** não continha uma junção, uma cláusula **Union** ou uma cláusula **Group by** ; e todas as colunas que usaram um alias ou uma expressão na lista de seleção não foram associadas a **SQLBindCol**.  
  
-   Se o driver oferecer suporte a apenas uma instrução ativa, a biblioteca de cursores buscará o restante do conjunto de resultados antes de executar a instrução **Select** e chamar **SQLGetData**.
