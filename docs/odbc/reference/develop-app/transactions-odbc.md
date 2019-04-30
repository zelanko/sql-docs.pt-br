---
title: Transações ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6ce5decd2744c0ce9d753e355321a40d00fd620
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305808"
---
# <a name="transactions-odbc"></a>Transações ODBC
Um *transação* é uma unidade de trabalho que é feito como uma única operação atômica; ou seja, a operação for bem-sucedida ou falha como um todo. Por exemplo, considere transferir dinheiro de uma conta bancária para outra. Isso envolve duas etapas: Retirando o dinheiro da primeira conta e depositando-lo no segundo. É importante que as duas etapas é bem-sucedida; não é aceitável para uma etapa seja bem-sucedida e a outra falhe. Um banco de dados que oferece suporte a transações é capaz de garantir isso.  
  
 As transações podem ser concluídas por sendo *confirmada* ou que está sendo *revertida*. Quando uma transação é confirmada, as alterações feitas em que a transação se tornam permanentes. Quando uma transação for revertida, as linhas afetadas são retornadas para o estado em que estavam antes que a transação foi iniciada. Para estender o exemplo de transferência de conta, um aplicativo executa uma instrução SQL para a primeira conta de débito e uma instrução SQL diferente para a segunda conta de crédito. Se as duas instruções forem bem-sucedidas, o aplicativo, em seguida, confirma a transação. Mas, se a instrução falhar por algum motivo, o aplicativo será revertida a transação. Em ambos os casos, o aplicativo garante um estado consistente no final da transação.  
  
 Uma única transação pode abranger várias operações de banco de dados que ocorrem em momentos diferentes. Se outras transações tivessem acesso completo para os resultados intermediários, as transações podem interferir uns com os outros. Por exemplo, suponha que uma transação insere uma linha, uma segunda transação lê nessa linha e a primeira transação será revertida. A segunda transação agora tem dados de uma linha que não existe.  
  
 Para resolver esse problema, há vários esquemas para isolar as transações uns dos outros. *Isolamento de transação* geralmente é implementado pelo bloqueio de linhas, que impede a mais de uma transação que usa a mesma linha ao mesmo tempo. Em alguns bancos de dados, o bloqueio de uma linha poderá também bloquear outras linhas.  
  
 Com transação maior isolamento vem reduzido *simultaneidade,* ou a capacidade de duas transações de usar os mesmos dados ao mesmo tempo. Para obter mais informações, consulte [definir o nível de isolamento da transação](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Transações em ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento de transação](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controle de simultaneidade](../../../odbc/reference/develop-app/concurrency-control.md)
