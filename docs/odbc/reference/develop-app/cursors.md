---
title: Cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c9179506ac96c1902c40de271f6024ed7e5c54d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001991"
---
# <a name="cursors"></a>Cursores
Um aplicativo busca os dados com um *cursor*. Um cursor é diferente de um conjunto de resultados: Um conjunto de resultados é o conjunto de linhas que corresponde aos critérios de pesquisa específica, enquanto que um cursor é o software que retorna as linhas para o aplicativo. O nome *cursor,* como ele se aplica aos bancos de dados, provavelmente foi originado o cursor piscando em um terminal do computador. Assim como o cursor indica a posição atual na tela e onde as palavras digitadas aparecerá próximo, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados e quais linhas serão retornadas em seguida.  
  
 O modelo de cursor ODBC baseia-se no modelo de cursor no embedded SQL. Uma diferença importante entre esses modelos é que as maneira como cursores são abertos. No embedded SQL, um cursor deve ser explicitamente declarado e aberto antes que ele pode ser usado. No ODBC, um cursor é aberto implicitamente quando uma instrução que cria um conjunto de resultados é executada. Quando o cursor é aberto, ele é posicionado antes da primeira linha do conjunto de resultados. No embedded SQL e ODBC, um cursor deve ser fechado depois que o aplicativo terminar de usá-lo.  
  
 Cursores diferentes têm características diferentes. O tipo mais comum de cursor, que é chamado de um *cursor de somente avanço,* só pode mover para frente por meio do conjunto de resultados. Para retornar a uma linha anterior, o aplicativo feche e reabra o cursor e, em seguida, ler linhas desde o início do resultado definido até atingir a linha necessária. Cursores de somente avanço fornecem um mecanismo rápido para fazer uma única passagem por meio de um conjunto de resultados.  
  
 Cursores de somente avanço são menos útil para aplicativos baseados em tela, em que o usuário rola para trás e encaminhar os dados. Esses aplicativos podem usar um cursor de somente avanço lendo o resultado definido uma vez, armazenar em cache os dados localmente e execução de rolagem em si. No entanto, isso funciona bem apenas com pequenas quantidades de dados. Uma solução melhor é usar um *cursor rolável,* que fornece acesso aleatório ao conjunto de resultados. Tais aplicativos também podem melhorar desempenho ao buscar mais de uma linha de dados de cada vez, usando o que é chamado um *cursor em bloco.* Para obter mais informações sobre cursores em bloco, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 O cursor de somente avanço é o tipo de cursor padrão no ODBC e é discutido nas seções a seguir. Para obter mais informações sobre cursores roláveis e cursores em bloco, consulte [cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md) e [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Confirmar ou reverter uma transação, ou explicitamente chamando **SQLEndTran** ou pelo operando no modo de confirmação automática, faz com que algumas fontes de dados fechar todos os cursores em todas as instruções em uma conexão. Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR a [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função.
