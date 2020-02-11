---
title: Atualizando dados com o SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2895ec765df3910dbbaa1e76ba1579e4afe5cca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091649"
---
# <a name="updating-data-with-sqlsetpos"></a>Atualizar dados com SQLSetPos
Os aplicativos podem atualizar ou excluir qualquer linha no conjunto de linhas com **SQLSetPos**. Chamar **SQLSetPos** é uma alternativa conveniente para construir e executar uma instrução SQL. Ele permite que um driver ODBC dê suporte a atualizações posicionadas mesmo quando a fonte de dados não oferece suporte a instruções SQL posicionadas. Ele faz parte do paradigma da obtenção de acesso completo ao banco de dados por meio de chamadas de função.  
  
 **SQLSetPos** opera no conjunto de linhas atual e pode ser usado somente após uma chamada para **SQLFetchScroll**. O aplicativo especifica o número da linha a ser atualizada, excluída ou inserida, e o driver recupera os novos dados para essa linha dos buffers de conjunto de linhas. **SQLSetPos** também pode ser usado para designar uma linha especificada como a linha atual ou para atualizar uma linha específica no conjunto de linhas da fonte de dados.  
  
 O tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_ROW_ARRAY_SIZE. O **SQLSetPos** usa um novo tamanho de conjunto de linhas, no entanto, somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Por exemplo, se o tamanho do conjunto de linhas for alterado, **SQLSetPos** será chamado e, em seguida, **SQLFetch** ou **SQLFetchScroll** será chamado e a chamada para **SQLSetPos** usará o tamanho do conjunto de linhas antigo, enquanto **SQLFetch** ou **SQLFetchScroll** usará o novo tamanho do conjunto de linhas.  
  
 A primeira linha do conjunto de linhas é o número de linha 1. O argumento *RowNumber* em **SQLSetPos** deve identificar uma linha no conjunto de linhas; ou seja, seu valor deve estar no intervalo entre 1 e o número de linhas que foram buscadas mais recentemente (o que pode ser menor que o tamanho do conjunto de linhas). Se *RowNumber* for 0, a operação se aplicará a todas as linhas no conjunto de linhas.  
  
 Como a maior parte da interação com bancos de dados relacionais é feita por meio do SQL, o **SQLSetPos** não é amplamente suportado. No entanto, um driver pode facilmente emular, construindo e executando uma instrução **Update** ou **delete** .  
  
 Para determinar a quais operações o **SQLSetPos** dá suporte, um aplicativo chama **SQLGetInfo** com a opção SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 informações (dependendo do tipo do cursor).  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Atualizar linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Excluir linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
