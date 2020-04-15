---
title: Atualizando dados com SQLSetPos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16476a1e1007905f34ec2e70ce6032eb8d81fe7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286156"
---
# <a name="updating-data-with-sqlsetpos"></a>Atualizar dados com SQLSetPos
Os aplicativos podem atualizar ou excluir qualquer linha no conjunto de linhas com **SQLSetPos**. Chamar **SQLSetPos** é uma alternativa conveniente para construir e executar uma declaração SQL. Ele permite que um driver oDBC suporte a atualizações posicionadas mesmo quando a fonte de dados não suporta instruções SQL posicionadas. Faz parte do paradigma de alcançar o acesso completo ao banco de dados por meio de chamadas de função.  
  
 **O SQLSetPos** opera no conjunto de linhas atual e só pode ser usado após uma chamada para **SQLFetchScroll**. O aplicativo especifica o número da linha para atualizar, excluir ou inserir e o driver recupera os novos dados dessa linha a partir dos buffers do conjunto de linhas. **SQLSetPos** também pode ser usado para designar uma linha especificada como a linha atual ou para atualizar uma linha específica no conjunto de linhas a partir da fonte de dados.  
  
 O tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa um novo tamanho de conjunto de linhas, no entanto, somente após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Por exemplo, se o tamanho do conjunto de linhas for alterado, **o SQLSetPos** é chamado e, em seguida, **sQLFetchou-se** é chamado, e a chamada para **SQLSetPos** usa o tamanho antigo do conjunto de linhas, enquanto **SQLFetch** ou **SQLFetchScroll** usa o novo tamanho de conjunto de linhas. **SQLFetchScroll**  
  
 A primeira linha do conjunto de linhas é o número de linha 1. O argumento *'Número de* linhas' no **SQLSetPos** deve identificar uma linha no conjunto de linhas; ou seja, seu valor deve estar na faixa entre 1 e o número de linhas que foram mais recentemente buscadas (que podem ser menores do que o tamanho do rowset). Se *O Número de* linhas for 0, a operação se aplica a todas as linhas do conjunto de linhas.  
  
 Como a maior parte da interação com bancos de dados relacionais é feita através do SQL, **o SQLSetPos** não é amplamente suportado. No entanto, um driver pode facilmente emulá-lo construindo e executando uma **declaração UPDATE** ou **DELETE.**  
  
 Para determinar quais operações **o SQLSetPos** suporta, um aplicativo chama **sqlgetinfo** com a opção de informações SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Atualizar linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [Excluir linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
