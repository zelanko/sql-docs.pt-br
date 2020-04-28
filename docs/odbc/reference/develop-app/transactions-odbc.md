---
title: ODBC de transações | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297951"
---
# <a name="transactions-odbc"></a>Transações ODBC
Uma *transação* é uma unidade de trabalho que é feita como uma única operação atômica; ou seja, a operação é bem-sucedida ou falha como um todo. Por exemplo, considere transferir dinheiro de uma conta bancária para outra. Isso envolve duas etapas: retirando o dinheiro da primeira conta e depositando-o no segundo. É importante que ambas as etapas tenham sucesso; Não é aceitável que uma etapa seja bem-sucedida e a outra falhe. Um banco de dados que dá suporte a transações é capaz de garantir isso.  
  
 As transações podem ser concluídas por serem *confirmadas* ou sendo *revertidas*. Quando uma transação é confirmada, as alterações feitas nessa transação tornam-se permanentes. Quando uma transação é revertida, as linhas afetadas são retornadas para o estado em que estavam antes da transação ser iniciada. Para estender o exemplo de transferência de conta, um aplicativo executa uma instrução SQL para debitar a primeira conta e uma instrução SQL diferente para creditar a segunda conta. Se ambas as instruções tiverem sucesso, o aplicativo confirmará a transação. Mas se uma das instruções falhar por algum motivo, o aplicativo reverterá a transação. Em ambos os casos, o aplicativo garante um estado consistente no final da transação.  
  
 Uma única transação pode abranger várias operações de banco de dados que ocorrem em momentos diferentes. Se outras transações tivessem acesso total aos resultados intermediários, as transações podem interferir umas com as outras. Por exemplo, suponha que uma transação insira uma linha, uma segunda transação Leia essa linha e a primeira transação seja revertida. A segunda transação agora tem dados para uma linha que não existe.  
  
 Para resolver esse problema, há vários esquemas para isolar as transações uns dos outros. O *isolamento de transação* geralmente é implementado por meio do bloqueio de linhas, o que impede que mais de uma transação use a mesma linha ao mesmo tempo. Em alguns bancos de dados, bloquear uma linha também pode bloquear outras linhas.  
  
 Com o maior isolamento de transação vem com uma *simultaneidade* reduzida ou a capacidade de duas transações usarem os mesmos dados ao mesmo tempo. Para obter mais informações, consulte [definindo o nível de isolamento da transação](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Transações em ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento de transação](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controle de simultaneidade](../../../odbc/reference/develop-app/concurrency-control.md)
