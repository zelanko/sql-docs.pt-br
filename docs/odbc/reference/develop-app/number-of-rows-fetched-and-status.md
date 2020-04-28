---
title: Número de linhas buscadas e status | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20e1632e8da765b0da2785bd846b67d13ebe01ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302357"
---
# <a name="number-of-rows-fetched-and-status"></a>Número de linhas buscadas e status
Se o atributo da instrução SQL_ATTR_ROWS_FETCHED_PTR tiver sido definido, ele especificará um buffer que retorna o número de linhas buscadas pela chamada para **SQLFetch** ou **SQLFetchScroll**e linhas de erro. (Esse número é uma contagem de todas as linhas que não têm o status SQL_ROW_NO_ROWS.) Após uma chamada para **SQLBulkOperations** ou **SQLSetPos**, o buffer contém o número de linhas que foram afetadas por uma operação em massa executada pela função. Se o atributo de instrução SQL_ATTR_ROW_STATUS_PTR tiver sido definido, **SQLFetch** ou **SQLFetchScroll** retornará a *matriz de status de linha,* que fornece o status de cada linha retornada. Os dois buffers apontados por esses campos são alocados pelo aplicativo e preenchidos pelo driver. Um aplicativo deve garantir que esses ponteiros permaneçam válidos até que o cursor seja fechado.  
  
 Entradas na linha status da matriz definem se cada linha foi buscada com êxito, se ela foi atualizada, adicionada ou excluída desde a última busca e se ocorreu um erro ao buscar a linha. Se **SQLFetch** ou **SQLFetchScroll** encontrar um erro ao recuperar uma linha de um conjunto de linhas de LinhaMúltipla ou se **SQLBulkOperations** com um argumento de *operação* de SQL_FETCH_BY_BOOKMARK encontrar um erro ao executar uma busca em massa, ele definirá o valor correspondente na matriz de status de linha como SQL_ROW_ERROR, continuará buscando linhas e retornará SQL_SUCCESS_WITH_INFO. Para obter mais informações sobre o tratamento de erros e a matriz de status de linha, consulte as descrições de função [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) e [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) .
