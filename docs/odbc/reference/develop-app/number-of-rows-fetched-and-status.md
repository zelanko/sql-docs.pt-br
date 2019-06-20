---
title: Número de linhas buscadas e Status | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab4830ddd56335959dd7049a1dabdcc3a0354213
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149326"
---
# <a name="number-of-rows-fetched-and-status"></a>Número de linhas buscadas e status
Se o atributo SQL_ATTR_ROWS_FETCHED_PTR de instrução tiver sido definido, ele especifica um buffer que retorna o número de linhas buscadas pela chamada para **SQLFetch** ou **SQLFetchScroll**e linhas de erro. (Esse número é uma contagem de todas as linhas que não têm o status SQL_ROW_NO_ROWS.) Após uma chamada para **SQLBulkOperations** ou **SQLSetPos**, o buffer contém o número de linhas que foram afetados por uma operação em massa executada pela função. Se o atributo da instrução SQL_ATTR_ROW_STATUS_PTR tiver sido definido, **SQLFetch** ou **SQLFetchScroll** retorna o *matriz de status de linha,* que fornece o status de cada linha retornada. Ambos os buffers apontados por esses campos são alocados pelo aplicativo e preenchidos pelo driver. Um aplicativo deve se certificar de que esses ponteiros permanecem válidos até que o cursor seja fechado.  
  
 Entradas no estado de matriz de status de linha se cada linha foi buscada com êxito, se ele foi atualizado, adicionado ou excluído desde que foi buscada pela última vez e se ocorreu um erro ao buscar a linha. Se **SQLFetch** ou **SQLFetchScroll** encontra um erro ao recuperar uma linha de um conjunto de linhas de várias linhas, ou se **SQLBulkOperations** com um *operação*  argumento de SQL_FETCH_BY_BOOKMARK encontra um erro ao executar uma busca em massa, ele define o valor correspondente na matriz de status de linha para SQL_ROW_ERROR, continua a busca de linhas e retorna SQL_SUCCESS_WITH_INFO. Para obter mais informações sobre o tratamento de erros e a matriz de status de linha, consulte o [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) e [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) descrições de função.
