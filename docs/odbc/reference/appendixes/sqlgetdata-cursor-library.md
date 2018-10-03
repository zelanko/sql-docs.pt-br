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
manager: craigg
ms.openlocfilehash: 1e3009b4e3bed6fc871ecfd1aab4e2af2f1f1c86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853994"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLGetData** função na biblioteca de cursor. Para obter informações gerais sobre **SQLGetData**, consulte [função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 A biblioteca de cursores implementa **SQLGetData** criando primeiro uma **selecionar** instrução com uma **onde** cláusula que enumera os valores armazenados em seu cache para cada limite coluna na linha atual. Em seguida, ele executa o **selecionar** instrução selecionar novamente a linha e chama **SQLGetData** no driver para recuperar os dados da fonte de dados (em vez do cache).  
  
> [!CAUTION]  
>  O **onde** cláusula construída pela biblioteca de cursores para identificar a linha atual pode não conseguir identificar todas as linhas, identifique uma linha diferente ou identificar mais de uma linha. Para obter mais informações, consulte [construindo instruções pesquisadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Se o atributo da instrução SQL_ATTR_USE_BOOKMARKS for definido como SQL_UB_VARIABLE, **SQLGetData** pode ser chamado na coluna 0 para retornar dados de indicador.  
  
 Chamadas para **SQLGetData** estão sujeitos às seguintes restrições:  
  
-   **SQLGetData** não pode ser chamado para cursores de somente avanço.  
  
-   **SQLGetData** pode ser chamado somente quando as seguintes condições forem atendidas: uma **selecionar** instrução gerou o conjunto de resultados; a **selecionar** instrução não continha uma junção, um  **União** cláusula, ou um **GROUP BY** cláusula; e todas as colunas que é usado um alias ou uma expressão na lista de seleção não foram vinculadas com **SQLBindCol**.  
  
-   Se o driver dá suporte a apenas uma instrução ativa, a biblioteca de cursores busca o restante do conjunto de resultados antes de executar o **selecionar** instrução e chamar **SQLGetData**.
