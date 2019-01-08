---
title: Cursores roláveis | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80be6994c7094b365bc24dd135bdda6ec4e561ab
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513484"
---
# <a name="scrollable-cursors"></a>Cursores roláveis
Em aplicativos modernos baseados em tela, o usuário rola para trás e para frente por meio dos dados. Para tais aplicativos, retornando a uma linha extraída anteriormente é um problema. Uma possibilidade é feche e reabra o cursor e, em seguida, buscar linhas até que o cursor atinge a linha necessária. Outra possibilidade é ler o conjunto de resultados, o armazena em cache localmente e implementar a rolagem no aplicativo. Ambas as possibilidades funcionam bem somente com conjuntos de resultados pequenos e a segunda possibilidade é difícil de implementar. Uma solução melhor é usar um *cursor rolável,* que pode mover para trás e para a frente no conjunto de resultados.  
  
 Um *cursor rolável* é comumente usado em aplicativos modernos baseados em tela, no qual o usuário rola para frente e para trás por meio dos dados. No entanto, aplicativos devem usar cursores roláveis somente quando cursores de somente avanço não fará o trabalho, como cursores roláveis são geralmente mais caros do que cursores de somente avanço.  
  
 A capacidade de retroceder levanta uma pergunta não é aplicável a cursores de somente avanço: Um cursor rolável deve detectar as alterações feitas em linhas buscadas anteriormente? Ou seja, ele deve detectar linhas recentemente inseridas atualizadas e excluídas?  
  
 Essa pergunta surge porque a definição de um conjunto de resultados – o conjunto de linhas que corresponda a determinados critérios - não informa quando linhas são verificadas para ver se elas correspondem a esses critérios, nem faz isso de estado se linhas devem conter os mesmos dados toda vez que elas sejam buscadas. A omissão antiga torna possível para cursores roláveis detectar se linhas foram inseridas ou excluídas, enquanto o último torna possível para que eles possam detectar dados atualizados.  
  
 A capacidade de detectar alterações às vezes é útil, às vezes, não. Por exemplo, um aplicativo de contabilidade precisa de um cursor que ignora todas as alterações; livros de balanceamento é impossível se o cursor mostra as alterações mais recentes. Por outro lado, um sistema de reserva de companhia aérea precisa de um cursor que mostra as alterações mais recentes para os dados. sem cursor, ele deve repetir continuamente o banco de dados para mostrar a disponibilidade mais atualizada de voo.  
  
 Para abordar as necessidades de diferentes aplicativos, o ODBC define quatro tipos diferentes de cursores roláveis. Esses cursores variam em despesas e em sua capacidade de detectar alterações para o resultado definido. Observe que se um cursor rolável pode detectar alterações em linhas, ele só pode detectá-los quando ele tenta buscar essas linhas; Não há nenhuma maneira para a fonte de dados para notificar o cursor de alterações a linhas buscadas atualmente. Observe também que a visibilidade das alterações também é controlada pelo nível de isolamento da transação; Para obter mais informações, consulte [isolamento da transação](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de cursor rolável](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Usando cursores roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Rolagem relativa e absoluta](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
