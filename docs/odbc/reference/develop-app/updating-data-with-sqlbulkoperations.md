---
title: Atualizando dados com o SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b96e3a43b8385910e4260cf51dea7e4ff508200
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298480"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Atualizar dados com SQLBulkOperations
Os aplicativos podem executar operações de atualização, exclusão, busca ou inserção em massa na tabela subjacente na fonte de dados com uma chamada para **SQLBulkOperations**. Chamar **SQLBulkOperations** é uma alternativa conveniente para construir e executar uma instrução SQL. Ele permite que um driver ODBC dê suporte a atualizações posicionadas mesmo quando a fonte de dados não oferece suporte a instruções SQL posicionadas. Ele faz parte do paradigma da obtenção de acesso completo ao banco de dados por meio de chamadas de função.  
  
 **SQLBulkOperations** opera no conjunto de linhas atual e pode ser usado somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**. O aplicativo especifica as linhas a serem atualizadas, excluídas ou atualizadas armazenando em cache seus indicadores. O driver recupera os novos dados para as linhas a serem atualizadas ou os novos dados a serem inseridos na tabela subjacente, dos buffers de conjunto de linhas.  
  
 O tamanho do conjunto de linhas a ser usado pelo **SQLBulkOperations** é definido por uma chamada para **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_ROW_ARRAY_SIZE. Ao contrário de **SQLSetPos**, que usa um novo tamanho de conjunto de linhas somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**, **SQLBulkOperations** usa o novo tamanho do conjunto de linhas após a chamada para **SQLSetStmtAttr**.  
  
 Como a maior parte da interação com bancos de dados relacionais é feita por meio do SQL, o **SQLBulkOperations** não é amplamente suportado. No entanto, um driver pode facilmente emular, construindo e executando uma instrução **Update**, **delete**ou **Insert** .  
  
 Para determinar a quais operações o **SQLBulkOperation** dá suporte, um aplicativo chama **SQLGetInfo** com a opção SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 informações (dependendo do tipo do cursor).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Atualizar linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Excluir linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserir linhas com SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Buscar linhas com SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
