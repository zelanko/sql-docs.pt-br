---
title: Tamanho do conjunto de linhas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 42870c60bfec0911b1a676b090a7d94bd5f42d1a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="rowset-size"></a>Tamanho do conjunto de linhas
O tamanho do conjunto de linhas a ser usado depende do aplicativo. Aplicativos baseados em tela comumente siga uma das duas estratégias. A primeira é para definir o tamanho do conjunto de linhas para o número de linhas exibidas na tela; Se o usuário o redimensiona a tela, o aplicativo altera o tamanho do conjunto de linhas adequadamente. A segunda é definir o tamanho do conjunto de linhas para um número maior, como 100, que reduz o número de chamadas para a fonte de dados. O aplicativo localmente rola dentro do conjunto de linhas quando possível e busca de novas linhas apenas quando ele rola fora do conjunto de linhas.  
  
 Outros aplicativos, como relatórios, tendem a definir o tamanho do conjunto de linhas para o maior número de linhas que o aplicativo pode manipular razoavelmente — com um conjunto de linhas maior, a rede sobrecarga por linha, às vezes, é reduzida. Exatamente um conjunto de linhas como grande pode ser depende do tamanho de cada linha e a quantidade de memória disponível no.  
  
 Tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um *atributo* argumento de SQL_ATTR_ROW_ARRAY_SIZE. O aplicativo pode alterar o tamanho do conjunto de linhas, associar novos buffers de conjunto de linhas (chamando **SQLBindCol** ou especificando um deslocamento de associação) mesmo depois que linhas foram buscadas, ou ambos. As implicações de alterar o tamanho do conjunto de linhas dependem da função:  
  
-   **SQLFetch** e **SQLFetchScroll** usar o tamanho do conjunto de linhas no momento da chamada para determinar quantas linhas para buscar. No entanto, **SQLFetchScroll** com um *FetchOrientation* de incrementos SQL_FETCH_NEXT o cursor com base no conjunto de linhas de busca anterior e, em seguida, busca um conjunto de linhas com base no tamanho atual do conjunto de linhas.  
  
-   **SQLSetPos** usa o tamanho de conjunto de linhas está em vigor a partir de uma chamada anterior para **SQLFetch** ou **SQLFetchScroll**, pois **SQLSetPos** opera em um conjunto de linhas que já foi definido. **SQLSetPos** também escolherá o novo tamanho do conjunto de linhas se **SQLBulkOperations** foi chamado depois que o tamanho do conjunto de linhas foi alterado.  
  
-   **SQLBulkOperations** usa o tamanho do conjunto de linhas em vigor no momento da chamada, porque ele executa as operações em uma tabela independente de qualquer conjunto de linhas busca.
