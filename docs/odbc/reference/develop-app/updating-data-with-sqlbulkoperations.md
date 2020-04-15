---
title: Atualização de dados com SQLBulkOperations | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298480"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Atualizar dados com SQLBulkOperations
Os aplicativos podem executar operações de atualização em massa, exclusão, busca ou inserção na tabela subjacente na fonte de dados com uma chamada para **SQLBulkOperations**. Chamar **a SQLBulkOperations** é uma alternativa conveniente para construir e executar uma declaração SQL. Ele permite que um driver oDBC suporte a atualizações posicionadas mesmo quando a fonte de dados não suporta instruções SQL posicionadas. Faz parte do paradigma de alcançar o acesso completo ao banco de dados por meio de chamadas de função.  
  
 **SQLBulkOperations** opera no conjunto de linhas atual e só pode ser usado após uma chamada para **SQLFetch** ou **SQLFetchScroll**. O aplicativo especifica as linhas para atualizar, excluir ou atualizar, registrando seus marcadores. O driver recupera os novos dados para que as linhas sejam atualizadas ou os novos dados a serem inseridos na tabela subjacente, a partir dos buffers de conjunto de linhas.  
  
 O tamanho do conjunto de linhas a ser usado pelo **SQLBulkOperations** é definido por uma chamada para **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_ROW_ARRAY_SIZE. Ao contrário **do SQLSetPos,** que usa um novo tamanho de conjunto de linhas somente após uma chamada para **SQLFetch** ou **SQLFetchScroll,** **a SQLBulkOperations** usa o novo tamanho de conjunto de linhas após a chamada para **SQLSetStmtAttr**.  
  
 Como a maior parte da interação com bancos de dados relacionais é feita através do SQL, **o SQLBulkOperations** não é amplamente suportado. No entanto, um driver pode facilmente emulá-lo construindo e executando uma instrução **UPDATE,** **DELETE**ou **INSERT.**  
  
 Para determinar quais operações o **SQLBulkOperation** suporta, um aplicativo chama **SQLGetInfo** com a opção de SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Atualizar linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Excluir linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserir linhas com SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Buscar linhas com SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
