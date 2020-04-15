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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304237"
---
# <a name="rowset-size"></a>Tamanho do conjunto de linhas
Qual tamanho de conjunto de linhas para usar depende da aplicação. Aplicativos baseados em tela geralmente seguem uma das duas estratégias. A primeira é definir o tamanho do conjunto de linhas para o número de linhas exibidas na tela; se o usuário redimensionar a tela, o aplicativo altera o tamanho do conjunto de linhas de acordo. A segunda é definir o tamanho do conjunto de linhas para um número maior, como 100, o que reduz o número de chamadas para a fonte de dados. O aplicativo rola localmente dentro do conjunto de linhas quando possível e busca novas linhas somente quando rola para fora do conjunto de linhas.  
  
 Outros aplicativos, como relatórios, tendem a definir o tamanho do conjunto de linhas para o maior número de linhas que o aplicativo pode lidar razoavelmente - com um conjunto de linhas maior, a sobrecarga de rede por linha às vezes é reduzida. Exatamente o tamanho de um conjunto de linhas depende do tamanho de cada linha e da quantidade de memória disponível.  
  
 O tamanho do conjunto de linhas é definido por uma chamada para **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_ROW_ARRAY_SIZE. O aplicativo pode alterar o tamanho do conjunto de linhas, vincular novos buffers de conjunto de linhas (ligando para **SQLBindCol** ou especificando um deslocamento de vinculação) mesmo depois que as linhas forem buscadas, ou ambas. As implicações de alterar o tamanho do conjunto de linhas dependem da função:  
  
-   **SQLFetch** e **SQLFetchScroll** usam o tamanho do conjunto de linhas no momento da chamada para determinar quantas linhas buscar. No entanto, **sqlfetchscroll** com uma *Orientação fetch* de SQL_FETCH_NEXT incrementa o cursor com base no conjunto de linhas da busca anterior e, em seguida, busca um conjunto de linhas com base no tamanho atual do conjunto de linhas.  
  
-   **O SQLSetPos** usa o tamanho do conjunto de linhas que está em vigor a partir da chamada anterior para **SQLFetch** ou **SQLFetchScroll,** porque **o SQLSetPos** opera em um conjunto de linhas que já foi definido. **SQLSetPos** também pegará o novo tamanho de conjunto de linhas se **o SQLBulkOperations** tiver sido chamado depois que o tamanho do conjunto de linhas foi alterado.  
  
-   **A SQLBulkOperations** usa o tamanho do conjunto de linhas em vigor no momento da chamada, porque executa operações em uma tabela independente de qualquer conjunto de linhas buscadas.
