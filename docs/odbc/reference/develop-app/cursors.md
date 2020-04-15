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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305287"
---
# <a name="cursors"></a>Cursores
Um aplicativo busca dados com um *cursor*. Um cursor é diferente de um conjunto de resultados: Um conjunto de resultados é o conjunto de linhas que corresponde a determinados critérios de pesquisa, enquanto um cursor é o software que retorna essas linhas para o aplicativo. O *cursor de nome,* como se aplica aos bancos de dados, provavelmente se originou do cursor piscando em um terminal de computador. Assim como o cursor indica a posição atual na tela e onde as palavras digitadas aparecerão em seguida, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados e qual linha será devolvida em seguida.  
  
 O modelo de cursor em ODBC é baseado no modelo de cursor em SQL incorporado. Uma diferença notável entre esses modelos é a forma como os cursores são abertos. No SQL incorporado, um cursor deve ser explicitamente declarado e aberto antes de ser usado. No ODBC, um cursor é aberto implicitamente quando uma declaração que cria um conjunto de resultados é executada. Quando o cursor é aberto, ele é posicionado antes da primeira linha do conjunto de resultados. Tanto em SQL quanto em ODBC incorporados, um cursor deve ser fechado após o aplicativo ter terminado de usá-lo.  
  
 Diferentes cursores têm características diferentes. O tipo mais comum de cursor, que é chamado *de cursor somente para frente,* só pode avançar através do conjunto de resultados. Para retornar a uma linha anterior, o aplicativo deve fechar e reabrir o cursor e, em seguida, ler linhas desde o início do conjunto de resultados até atingir a linha necessária. Os cursores somente para frente fornecem um mecanismo rápido para fazer uma única passagem através de um conjunto de resultados.  
  
 Os cursores somente para frente são menos úteis para aplicativos baseados em tela, nos quais o usuário rola para trás e para frente através dos dados. Esses aplicativos podem usar um cursor somente para frente lendo o conjunto de resultados uma vez, arquivar os dados localmente e realizar rolagem por si mesmos. No entanto, isso funciona bem apenas com pequenas quantidades de dados. Uma solução melhor é usar um *cursor rolável,* que fornece acesso aleatório ao conjunto de resultados. Esses aplicativos também podem aumentar o desempenho, obtendo mais de uma linha de dados por vez, usando o que é chamado de *cursor de bloco.* Para obter mais informações sobre cursores de bloco, consulte [Usando cursors de bloco](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 O cursor somente para frente é o tipo de cursor padrão no ODBC e é discutido nas seções a seguir. Para obter mais informações sobre cursores de bloco e cursores roláveis, consulte [Cursors de bloco](../../../odbc/reference/develop-app/block-cursors.md) e [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Cometer ou reverter uma transação, seja ligando explicitamente para **o SQLEndTran** ou operando no modo de confirmação automática, faz com que algumas fontes de dados fechem todos os cursores em todas as declarações em uma conexão. Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na descrição da função [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
