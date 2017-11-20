---
title: Atualizando dados com SQLBulkOperations | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75e5f954065c0b41935aa231c85c093d5ee10226
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlbulkoperations"></a>Atualizando dados com SQLBulkOperations
Aplicativos podem executar operações de atualização, exclusão, busca ou inserção em massa na tabela subjacente na fonte de dados com uma chamada para **SQLBulkOperations**. Chamando **SQLBulkOperations** é uma alternativa conveniente para construir e executar uma instrução SQL. Ele permite que um driver ODBC oferecem suporte a atualizações posicionadas mesmo quando a fonte de dados não dá suporte a instruções SQL posicionadas. Ele faz parte do paradigma de obter acesso completo do banco de dados por meio de chamadas de função.  
  
 **SQLBulkOperations** opera no conjunto de linhas atual e pode ser usado somente depois de uma chamada para **SQLFetch** ou **SQLFetchScroll**. O aplicativo especifica as linhas para atualizar, excluir ou atualizar armazenando seus indicadores. O driver recupera os novos dados de linhas a serem atualizados ou novos dados a serem inseridos na tabela base, dos buffers de conjunto de linhas.  
  
 O tamanho do conjunto de linhas a ser usado pelo **SQLBulkOperations** é definido por uma chamada para **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. Ao contrário de **SQLSetPos**, que usa um novo tamanho do conjunto de linhas apenas após uma chamada para **SQLFetch** ou **SQLFetchScroll**, **SQLBulkOperations** usa o novo tamanho do conjunto de linhas após a chamada a **SQLSetStmtAttr**.  
  
 Como a interação com a maioria dos bancos de dados relacionais é feita por meio do SQL, **SQLBulkOperations** não tem muito suporte. No entanto, um driver pode facilmente emulá-lo criando e executando um **atualização**, **excluir**, ou **inserir** instrução.  
  
 Para determinar quais operações **SQLBulkOperation** oferece suporte, um aplicativo chama **SQLGetInfo** com SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1 ou opção de informações de SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo de cursor).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Atualizando linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Excluindo linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserindo linhas com SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Buscando linhas com SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)

