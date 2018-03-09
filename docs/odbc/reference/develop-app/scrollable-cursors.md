---
title: "Cursores roláveis | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1992b3fc6d6013859c1bdd46d119f633db46acfc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="scrollable-cursors"></a>Cursores roláveis
Aplicativos modernos em tela, o usuário rola para trás e frente os dados. Para esses aplicativos, retornando a uma linha anteriormente busca é um problema. Uma possibilidade é feche e reabra o cursor e, em seguida, buscar linhas até que o cursor atinge a linha necessária. Outra possibilidade é ler o conjunto de resultados, armazenar em cache localmente e implementar a rolagem no aplicativo. Ambas as possibilidades funcionam bem somente com conjuntos de resultados pequenos e a segunda possibilidade é difícil de implementar. Uma solução melhor é usar um *cursor rolável,* que pode retroceder e Avançar no conjunto de resultados.  
  
 Um *cursor rolável* é comumente usado em aplicativos modernos em tela, em que o usuário rola para frente e para trás através dos dados. No entanto, aplicativos devem usar cursores roláveis somente quando cursores de somente avanço não fará o trabalho, como cursores roláveis são geralmente mais caros do que cursores de somente avanço.  
  
 A capacidade de mover para trás gera uma pergunta não aplicável para cursores de somente avanço: deve um cursor rolável detectar alterações feitas nas linhas buscadas anteriormente? Ou seja, ele deve detectar as linhas recentemente inseridas atualizadas e excluídas?  
  
 Essa pergunta surge porque a definição de um resultado definido — o conjunto de linhas que corresponde a certos critérios — não informa quando linhas são verificadas para ver se corresponde a esses critérios, nem estado se linhas devem conter os mesmos dados toda vez que sejam buscadas. A omissão antiga torna possível para cursores roláveis detectar se linhas foram inseridas ou excluídas, enquanto o último torna possível detectar dados atualizados.  
  
 A capacidade de detectar alterações às vezes é útil, às vezes, não. Por exemplo, um aplicativo de contabilidade precisa de um cursor que ignora todas as alterações; balanceamento manuais é impossível se o cursor mostra as alterações mais recentes. Por outro lado, um sistema de reserva aérea precisa de um cursor que mostra as alterações mais recentes para os dados. sem cursor, ele deve repetir continuamente o banco de dados para mostrar a disponibilidade de voo mais atualizada.  
  
 Para abranger as necessidades de aplicativos diferentes, o ODBC define quatro tipos diferentes de cursores roláveis. Esses cursores variam em despesas e em sua capacidade de detectar alterações para o resultado definido. Observe que se um cursor rolável pode detectar alterações em linhas, ele pode apenas detectá-los quando ele tenta buscar essas linhas; novamente não é possível para a fonte de dados para notificar o cursor de alterações para as linhas buscadas atualmente. Observe também que a visibilidade das alterações também é controlada pelo nível de isolamento da transação; Para obter mais informações, consulte [isolamento da transação](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de cursor rolável](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Usando cursores roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Rolagem relativa e absoluta](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
