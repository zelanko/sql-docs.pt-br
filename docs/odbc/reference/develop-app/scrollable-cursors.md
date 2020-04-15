---
title: Cursors roláveis | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304207"
---
# <a name="scrollable-cursors"></a>Cursores roláveis
Em aplicativos modernos baseados em tela, o usuário rola para trás e para frente através dos dados. Para tais aplicações, retornar a uma linha anteriormente buscada é um problema. Uma possibilidade é fechar e reabrir o cursor e, em seguida, buscar linhas até que o cursor atinja a linha necessária. Outra possibilidade é ler o conjunto de resultados, cache-lo localmente e implementar rolagem no aplicativo. Ambas as possibilidades funcionam bem apenas com pequenos conjuntos de resultados, e a última possibilidade é difícil de implementar. Uma solução melhor é usar um *cursor rolável,* que pode se mover para trás e para frente no conjunto de resultados.  
  
 Um *cursor rolável* é comumente usado em aplicativos modernos baseados em tela, nos quais o usuário rola para frente e para trás através dos dados. No entanto, os aplicativos devem usar cursores roláveis somente quando os cursores somente para a frente não fizerem o trabalho, já que os cursores roláveis são geralmente mais caros do que os cursores somente para a frente.  
  
 A capacidade de mover-se para trás levanta uma questão que não se aplica aos cursores somente para frente: Um cursor rolável deve detectar alterações feitas em linhas anteriormente buscadas? Ou seja, deve detectar linhas atualizadas, excluídas e recém-inseridas?  
  
 Esta pergunta surge porque a definição de um conjunto de resultados - o conjunto de linhas que corresponde a determinados critérios - não diz quando as linhas são verificadas para ver se correspondem a esses critérios, nem afirma se as linhas devem conter os mesmos dados cada vez que são buscadas. A omissão anterior permite que os cursores roláveis detectem se as linhas foram inseridas ou excluídas, enquanto a segunda permite que eles detectem dados atualizados.  
  
 A capacidade de detectar mudanças às vezes é útil, às vezes não. Por exemplo, um aplicativo de contabilidade precisa de um cursor que ignore todas as alterações; balanceamento de livros é impossível se o cursor mostra as últimas mudanças. Por outro lado, um sistema de reservas de companhias aéreas precisa de um cursor que mostre as últimas alterações nos dados; sem esse cursor, ele deve continuamente requery o banco de dados para mostrar a disponibilidade de voo mais atualizada.  
  
 Para cobrir as necessidades de diferentes aplicações, o ODBC define quatro tipos diferentes de cursores roláveis. Esses cursores variam tanto em despesas quanto em sua capacidade de detectar alterações no conjunto de resultados. Observe que se um cursor rolável pode detectar alterações nas linhas, ele só pode detectá-las quando tentar rebuscar essas linhas; não há como a fonte de dados notificar o cursor de alterações nas linhas atualmente buscadas. Observe também que a visibilidade das alterações também é controlada pelo nível de isolamento da transação; para obter mais informações, consulte [Transaction Isolation](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de cursor rolável](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Usar cursores roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Rolagem relativa e absoluta](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
