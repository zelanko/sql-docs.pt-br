---
title: Tamanho do conjunto de linhas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54da54a63fb1234478a3161cd46e7143258d2d65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468673"
---
# <a name="rowset-size"></a>Tamanho do conjunto de linhas
Qual tamanho de conjunto de linhas a ser usado depende do aplicativo. Aplicativos baseados em tela comumente siga uma das duas estratégias. A primeira é definir o tamanho do conjunto de linhas para o número de linhas exibidas na tela; Se o usuário redimensiona a tela, o aplicativo altera o tamanho do conjunto de linhas adequadamente. A segunda é definir o tamanho do conjunto de linhas para um número maior, como 100, que reduz o número de chamadas para a fonte de dados. O aplicativo localmente rola dentro do conjunto de linhas quando possível e busca de novas linhas somente quando ele rola fora do conjunto de linhas.  
  
 Outros aplicativos, como relatórios, tendem a definir o tamanho do conjunto de linhas para o maior número de linhas que o aplicativo pode manipular razoavelmente - com um conjunto de linhas maior, a rede sobrecarga por linha, às vezes, é reduzida. Exatamente um conjunto de linhas como grandes pode ser depende do tamanho de cada linha e a quantidade de memória disponível.  
  
 Tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. O aplicativo pode alterar o tamanho do conjunto de linhas, associar os buffers do novo conjunto de linhas (chamando **SQLBindCol** ou especificando um deslocamento de associação), mesmo depois de linhas foram buscadas, ou ambos. As implicações de alterar o tamanho do conjunto de linhas dependem da função:  
  
-   **SQLFetch** e **SQLFetchScroll** usar o tamanho de conjunto de linhas no momento da chamada para determinar quantas linhas para buscar. No entanto, **SQLFetchScroll** com um *FetchOrientation* de incrementos SQL_FETCH_NEXT o cursor com base no conjunto de linhas de busca anterior e, em seguida, busca um conjunto de linhas com base no tamanho atual do conjunto de linhas.  
  
-   **SQLSetPos** usa o tamanho do conjunto de linhas que entra em vigor a partir de uma chamada anterior para **SQLFetch** ou **SQLFetchScroll**, pois **SQLSetPos** opera em um conjunto de linhas que já foi definida. **SQLSetPos** também selecionará o novo tamanho do conjunto de linhas se **SQLBulkOperations** foi chamado depois que o tamanho do conjunto de linhas foi alterado.  
  
-   **SQLBulkOperations** usa o tamanho do conjunto de linhas em vigor no momento da chamada, pois ele executa operações em uma tabela independente de qualquer conjunto de linhas buscado.
