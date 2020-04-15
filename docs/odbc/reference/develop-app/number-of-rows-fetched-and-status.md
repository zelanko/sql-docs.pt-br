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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302357"
---
# <a name="number-of-rows-fetched-and-status"></a>Número de linhas buscadas e status
Se o atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR tiver sido definido, ele especificará um buffer que retorna o número de linhas buscadas pela chamada para **SQLFetch** ou **SQLFetchScroll**e linhas de erro. (Este número é uma contagem de todas as linhas que não têm o status SQL_ROW_NO_ROWS.) Após uma chamada para **SQLBulkOperations** ou **SQLSetPos,** o buffer contém o número de linhas que foram afetadas por uma operação em massa realizada pela função. Se o atributo de declaração SQL_ATTR_ROW_STATUS_PTR tiver sido definido, **SQLFetch** ou **SQLFetchScroll** retornarão a matriz de *status da linha,* que fornece o status de cada linha retornada. Ambos os buffers apontados por esses campos são alocados pelo aplicativo e preenchidos pelo driver. Um aplicativo deve certificar-se de que esses ponteiros permanecem válidos até que o cursor seja fechado.  
  
 As entradas na matriz de status da linha afirmam se cada linha foi detectada com sucesso, se foi atualizada, adicionada ou excluída desde a última vez que foi buscada, e se ocorreu um erro ao buscar a linha. Se **o SQLFetch** ou **o SQLFetchScroll** encontrarem um erro ao recuperar uma linha de um conjunto de linhas multirow, ou se **o SQLBulkOperations** com um argumento de *Operação* de SQL_FETCH_BY_BOOKMARK encontrar um erro durante a execução de uma busca em massa, ele define o valor correspondente na matriz de status da linha para SQL_ROW_ERROR, continua buscando linhas e retorna SQL_SUCCESS_WITH_INFO. Para obter mais informações sobre o manuseio de erros e a matriz de status da linha, consulte as descrições da função [SQLFetchE](../../../odbc/reference/syntax/sqlfetch-function.md) e [SQLFetchScroll.](../../../odbc/reference/syntax/sqlfetchscroll-function.md)
