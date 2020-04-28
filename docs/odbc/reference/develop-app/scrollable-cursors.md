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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304207"
---
# <a name="scrollable-cursors"></a>Cursores roláveis
Em aplicativos modernos baseados em tela, o usuário rola para trás e para frente pelos dados. Para esses aplicativos, retornar a uma linha previamente buscada é um problema. Uma possibilidade é fechar e reabrir o cursor e, em seguida, buscar linhas até que o cursor atinja a linha necessária. Outra possibilidade é ler o conjunto de resultados, armazená-lo em cache localmente e implementar a rolagem no aplicativo. Ambas as possibilidades funcionam bem apenas com pequenos conjuntos de resultados e a última possibilidade é difícil de implementar. Uma solução melhor é usar um *cursor rolável,* que pode voltar e avançar no conjunto de resultados.  
  
 Um *cursor rolável* geralmente é usado em aplicativos modernos baseados em tela nos quais o usuário rola para frente e para trás pelos dados. No entanto, os aplicativos devem usar cursores roláveis somente quando cursores somente de encaminhamento não farão o trabalho, já que os cursores roláveis são geralmente mais caros do que os cursores de somente avanço.  
  
 A capacidade de mover para trás gera uma pergunta não aplicável a cursores somente de encaminhamento: um cursor rolável detecta alterações feitas nas linhas previamente buscadas? Ou seja, ele deve detectar linhas atualizadas, excluídas e recentemente inseridas?  
  
 Essa questão surge porque a definição de um conjunto de resultados – o conjunto de linhas que corresponde a determinados critérios – não é o estado em que as linhas são verificadas para ver se correspondem a esses critérios, nem se as linhas devem conter os mesmos dados sempre que forem buscadas. A antiga omissão possibilita que os cursores roláveis detectem se as linhas foram inseridas ou excluídas, enquanto o último possibilita que eles detectem dados atualizados.  
  
 A capacidade de detectar alterações às vezes é útil, às vezes não. Por exemplo, um aplicativo de contabilidade precisa de um cursor que ignore todas as alterações; os livros de balanceamento são impossíveis se o cursor mostrar as alterações mais recentes. Por outro lado, um sistema de reserva de viagens precisa de um cursor que mostra as alterações mais recentes nos dados; sem esse cursor, ele deve repetir a repetição do banco de dados para mostrar a disponibilidade de voo mais atualizada.  
  
 Para abranger as necessidades de aplicativos diferentes, o ODBC define quatro tipos diferentes de cursores roláveis. Esses cursores variam em despesas e em sua capacidade de detectar alterações no conjunto de resultados. Observe que, se um cursor rolável puder detectar alterações em linhas, ele só poderá detectá-las quando tentar buscar novamente essas linhas; Não há como a fonte de dados notificar o cursor sobre as alterações nas linhas buscadas no momento. Observe bem que a visibilidade das alterações também é controlada pelo nível de isolamento da transação; para obter mais informações, consulte [isolamento de transação](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de cursor rolável](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Usar cursores roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Rolagem relativa e absoluta](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
