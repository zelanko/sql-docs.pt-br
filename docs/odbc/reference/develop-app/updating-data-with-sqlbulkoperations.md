---
title: Atualizando dados com SQLBulkOperations | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 958514adc02452cdc75a05e7ad28cd31f4e8e0e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632439"
---
# <a name="updating-data-with-sqlbulkoperations"></a>Atualizar dados com SQLBulkOperations
Aplicativos podem executar operações de atualização, exclusão, busca ou inserção em massa na tabela subjacente na fonte de dados com uma chamada para **SQLBulkOperations**. Chamando **SQLBulkOperations** é uma alternativa conveniente para construir e executar uma instrução SQL. Ele permite que um driver ODBC dão suporte a atualizações posicionadas até mesmo quando a fonte de dados não dá suporte a instruções de SQL posicionadas. Ele faz parte do paradigma de conseguir acesso completo de banco de dados por meio de chamadas de função.  
  
 **SQLBulkOperations** opera no conjunto de linhas atual e pode ser usado somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**. O aplicativo especifica as linhas para atualizar, excluir ou atualizar armazenando em cache seus indicadores. O driver recupera os novos dados de linhas a serem atualizadas, ou os novos dados a serem inseridos na tabela subjacente, dos buffers de conjunto de linhas.  
  
 O tamanho do conjunto de linhas a ser usado pelo **SQLBulkOperations** é definido por uma chamada para **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. Diferentemente **SQLSetPos**, que usa um novo tamanho do conjunto de linhas somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**, **SQLBulkOperations** usa o novo tamanho do conjunto de linhas após a chamada para **SQLSetStmtAttr**.  
  
 Como a maioria dos interação com bancos de dados relacionais é feita por meio do SQL, **SQLBulkOperations** não tem amplo suporte. No entanto, um driver pode facilmente emulá-la, construir e executar uma **atualização**, **excluir**, ou **inserir** instrução.  
  
 Para determinar quais operações **SQLBulkOperation** dá suporte, um aplicativo chama **SQLGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 a opção de informações (dependendo do tipo de cursor).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Atualizando linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Excluindo linhas por indicador com SQLBulkOperations](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [Inserindo linhas com SQLBulkOperations](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [Buscando linhas com SQLBulkOperations](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
