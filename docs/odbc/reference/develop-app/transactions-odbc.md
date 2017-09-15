---
title: "Transações ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d11b681fa324c2c0b514bfb43aa67d51ce19a1ba
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="transactions-odbc"></a>Transações ODBC
Um *transação* é uma unidade de trabalho que é feito como uma única operação atômica; ou seja, a operação for bem-sucedida ou falhar como um todo. Por exemplo, considere a transferência de dinheiro de uma conta bancária para outra. Isso envolve duas etapas: Retirando o dinheiro da primeira conta e depositando-lo no segundo. É importante que as duas etapas tiverem êxito; não é aceitável para uma etapa seja bem-sucedida e o outro falhar. Um banco de dados que oferece suporte a transações é capaz de garantir isso.  
  
 As transações podem ser concluídas por sendo *confirmada* ou sendo *revertida*. Quando uma transação for confirmada, as alterações feitas em que a transação se tornam permanentes. Quando uma transação for revertida, as linhas afetadas são retornadas para o estado em que estavam antes da transação foi iniciada. Para estender o exemplo de transferência de conta, um aplicativo executa uma instrução SQL para a primeira conta de débito e uma instrução SQL diferente para a segunda conta de crédito. Se ambas as instruções for bem-sucedida, o aplicativo, em seguida, confirma a transação. Mas se a instrução falhar por algum motivo, o aplicativo reverterá toda a transação. Em ambos os casos, o aplicativo garante um estado consistente no final da transação.  
  
 Uma única transação pode abranger várias operações de banco de dados que ocorrem em momentos diferentes. Se outras transações tivessem acesso completo aos resultados intermediários, as transações podem interferir em uma da outra. Por exemplo, suponha que uma transação insere uma linha, uma segunda transação lê essa linha e a primeira transação é revertida. A segunda transação agora tem dados de uma linha que não existe.  
  
 Para resolver esse problema, há vários esquemas para isolar transações uns dos outros. *Isolamento de transação* geralmente é implementado pelo bloqueio de linhas, que impede a mais de uma transação que usa a mesma linha ao mesmo tempo. Em alguns bancos de dados, o bloqueio de uma linha pode também bloquear outras linhas.  
  
 Com a transação maior isolamento vem reduzido *simultaneidade,* ou a capacidade de duas transações usam os mesmos dados ao mesmo tempo. Para obter mais informações, consulte [definir o nível de isolamento da transação](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Transações em ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento de transação](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controle de simultaneidade](../../../odbc/reference/develop-app/concurrency-control.md)
