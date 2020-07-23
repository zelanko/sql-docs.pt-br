---
title: Cursores (ODBC) | Microsoft Docs
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
ms.openlocfilehash: 3a7484de48edaecea56fc135ca3b803875f9557c
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977773"
---
# <a name="cursors"></a>Cursores
Um aplicativo busca dados com um *cursor*. Um cursor é diferente de um conjunto de resultados: um conjunto de resultados é o conjunto de linhas que corresponde a critérios de pesquisa específicos, enquanto que um cursor é o software que retorna essas linhas ao aplicativo. O cursor de nome *,* como se aplica aos bancos de dados, provavelmente originado do cursor piscando em um terminal de computador. Assim como esse cursor indica a posição atual na tela e onde as palavras digitadas aparecerão em seguida, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados e qual linha será retornada em seguida.  
  
 O modelo de cursor em ODBC é baseado no modelo de cursor no SQL inserido. Uma diferença notável entre esses modelos é a maneira como os cursores são abertos. No SQL inserido, um cursor deve ser declarado explicitamente e aberto antes que possa ser usado. No ODBC, um cursor é aberto implicitamente quando uma instrução que cria um conjunto de resultados é executada. Quando o cursor é aberto, ele é posicionado antes da primeira linha do conjunto de resultados. No SQL incorporado e no ODBC, um cursor deve ser fechado depois que o aplicativo terminar de usá-lo.  
  
 Cursores diferentes têm características diferentes. O tipo de cursor mais comum, que é chamado de *cursor de somente avanço,* só pode avançar pelo conjunto de resultados. Para retornar a uma linha anterior, o aplicativo deve fechar e reabrir o cursor e, em seguida, ler linhas desde o início do conjunto de resultados até atingir a linha necessária. Os cursores de somente avanço fornecem um mecanismo rápido para fazer uma passagem única por um conjunto de resultados.  
  
 Os cursores de somente avanço são menos úteis para aplicativos baseados em tela, nos quais o usuário rola para trás e para frente pelos dados. Esses aplicativos podem usar um cursor de somente avanço lendo o conjunto de resultados uma vez, armazenando os dados localmente em cache e executando a rolagem por conta própria. No entanto, isso funciona bem apenas com pequenas quantidades de dados. Uma solução melhor é usar um *cursor rolável,* que fornece acesso aleatório ao conjunto de resultados. Esses aplicativos também podem aumentar o desempenho buscando mais de uma linha de dados de cada vez, usando o que é chamado de *cursor de bloco.* Para obter mais informações sobre cursores de bloco, consulte [usando cursores de bloco](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 O cursor de somente avanço é o tipo de cursor padrão no ODBC e é discutido nas seções a seguir. Para obter mais informações sobre cursores de bloco e cursores roláveis, consulte Cursors de [bloco](../../../odbc/reference/develop-app/block-cursors.md) e [cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  A confirmação ou reversão de uma transação, seja chamando explicitamente **SQLEndTran** ou operando no modo de confirmação automática, faz com que algumas fontes de dados Fechem todos os cursores em todas as instruções em uma conexão. Para obter mais informações, consulte os atributos SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
