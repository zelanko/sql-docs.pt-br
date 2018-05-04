---
title: Cursores | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e83efd6239d49af2066bd39d244665a50fa7030
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cursors"></a>Cursores
Um aplicativo busca dados com um *cursor*. Um cursor é diferente de um conjunto de resultados: um conjunto de resultados é o conjunto de linhas que corresponde aos critérios de pesquisa específica, enquanto um cursor é o software que retorna as linhas para o aplicativo. O nome *cursor,* como ele se aplica aos bancos de dados, provavelmente foi originado do cursor piscando em um computador com terminal. Assim como o cursor indica a posição atual na tela e onde as palavras digitadas aparecerá próximas, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados e quais linhas serão retornadas em seguida.  
  
 O modelo de cursor em ODBC é baseado no modelo de cursor no embedded SQL. Uma diferença notável entre esses modelos é que os cursores de forma são abertos. No embedded SQL, um cursor deve ser declarado explicitamente e aberto antes de ser usada. No ODBC, um cursor é implicitamente aberto quando uma instrução que cria um conjunto de resultados é executada. Quando o cursor é aberto, ele está posicionado antes da primeira linha do conjunto de resultados. No embedded SQL e ODBC, um cursor deve ser fechado depois que o aplicativo terminar de usá-lo.  
  
 Cursores diferentes têm características diferentes. O tipo mais comum de cursor, que é chamado de um *cursor somente de avanço,* só pode avançar por meio do conjunto de resultados. Para retornar a uma linha anterior, o aplicativo deve fechar e reabrir o cursor e ler as linhas desde o início do resultado definido até atingir a linha necessária. Cursores de somente avanço fornecem um mecanismo rápido para fazer uma única passagem por meio de um conjunto de resultados.  
  
 Cursores de somente avanço são menos útil para aplicativos baseados em tela, em que o usuário rola para trás e encaminhar os dados. Esses aplicativos podem usar um cursor somente de avanço, a leitura do resultado definido uma vez, os dados localmente em cache e executar a rolagem se. No entanto, isso funciona bem somente com pequenas quantidades de dados. Uma solução melhor é usar um *cursor rolável,* que fornece acesso aleatório ao conjunto de resultados. Esses aplicativos podem também aumentar o desempenho em busca de mais de uma linha de dados ao mesmo tempo, usando o que é chamado um *cursor em bloco.* Para obter mais informações sobre cursores em bloco, consulte [cursores em bloco usando](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 O cursor somente de avanço é o tipo de cursor padrão no ODBC e é discutido nas seções a seguir. Para obter mais informações sobre cursores em bloco e cursores roláveis, consulte [cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md) e [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Confirmar ou reverter uma transação, ou explicitamente chamando **SQLEndTran** ou ao operar no modo de confirmação automática, faz com que algumas fontes de dados fechar todos os cursores em todas as instruções em uma conexão. Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
