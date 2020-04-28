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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11b95768934f96e1587b3c570b2510f3c2849239
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304237"
---
# <a name="rowset-size"></a>Tamanho do conjunto de linhas
O tamanho do conjunto de linhas a ser usado depende do aplicativo. Aplicativos baseados em tela normalmente seguem uma das duas estratégias. A primeira é definir o tamanho do conjunto de linhas para o número de linhas exibidas na tela; Se o usuário redimensionar a tela, o aplicativo alterará o tamanho do conjunto de linhas de acordo. A segunda é definir o tamanho do conjunto de linhas para um número maior, como 100, que reduz o número de chamadas para a fonte de dados. O aplicativo rola localmente no conjunto de linhas quando possível e busca novas linhas somente quando rola para fora do conjunto de linhas.  
  
 Outros aplicativos, como relatórios, tendem a definir o tamanho do conjunto de linhas para o maior número de linhas que o aplicativo pode lidar razoavelmente com um conjunto de linhas maior, às vezes, a sobrecarga de rede por linha é reduzida. O tamanho de cada linha e a quantidade de memória disponível é exatamente o maior número possível de um conjunto de linhas.  
  
 O tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_ROW_ARRAY_SIZE. O aplicativo pode alterar o tamanho do conjunto de linhas, associar novos buffers de conjunto de linhas (chamando **SQLBindCol** ou especificando um deslocamento de associação) mesmo após as linhas terem sido buscadas, ou ambos. As implicações de alterar o tamanho do conjunto de linhas dependem da função:  
  
-   **SQLFetch** e **SQLFetchScroll** usam o tamanho do conjunto de linhas no momento da chamada para determinar quantas linhas buscar. No entanto, **SQLFetchScroll** com um *FetchOrientation* de SQL_FETCH_NEXT incrementa o cursor com base no conjunto de linhas da busca anterior e, em seguida, busca um conjunto de linhas com base no tamanho atual do conjunto de linhas.  
  
-   **SQLSetPos** usa o tamanho do conjunto de linhas que está em vigor a partir da chamada anterior para **SQLFetch** ou **SQLFetchScroll**, pois **SQLSetPos** opera em um conjunto de linhas que já foi definido. **SQLSetPos** também obterá o novo tamanho do conjunto de linhas se **SQLBulkOperations** tiver sido chamado depois que o tamanho do conjunto de linhas for alterado.  
  
-   **SQLBulkOperations** usa o tamanho do conjunto de linhas em vigor no momento da chamada, pois ele executa operações em uma tabela independente de qualquer conjunto de linhas buscado.
