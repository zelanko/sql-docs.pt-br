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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297951"
---
# <a name="transactions-odbc"></a>Transações ODBC
Uma *transação* é uma unidade de trabalho que é feita como uma única operação atômica; ou seja, a operação consegue ou falha como um todo. Por exemplo, considere transferir dinheiro de uma conta bancária para outra. Isso envolve duas etapas: retirar o dinheiro da primeira conta e depositá-lo na segunda. É importante que ambas as etapas tenham êxito; não é aceitável que um passo tenha sucesso e o outro falhe. Um banco de dados que suporta transações é capaz de garantir isso.  
  
 As transações podem ser concluídas sendo *comprometidas* ou sendo *revertidas*. Quando uma transação é cometida, as alterações feitas nessa transação são permanentes. Quando uma transação é revertida, as linhas afetadas são devolvidas ao estado em que estavam antes da transação ser iniciada. Para estender o exemplo de transferência de conta, um aplicativo executa uma declaração SQL para debitar a primeira conta e uma declaração SQL diferente para creditar a segunda conta. Se ambas as declarações forem bem sucedidas, o aplicativo comete a transação. Mas se qualquer declaração falhar por qualquer motivo, o aplicativo reverte a transação. Em ambos os casos, o aplicativo garante um estado consistente no final da transação.  
  
 Uma única transação pode abranger várias operações de banco de dados que ocorrem em momentos diferentes. Se outras transações tivessem acesso completo aos resultados intermediários, as transações poderiam interferir entre si. Por exemplo, suponha que uma transação insere uma linha, uma segunda transação lê essa linha e a primeira transação é revertida. A segunda transação agora tem dados para uma linha que não existe.  
  
 Para resolver esse problema, existem vários esquemas para isolar transações entre si. *O isolamento de transações* é geralmente implementado por linhas de bloqueio, o que impede mais de uma transação de usar a mesma linha ao mesmo tempo. Em alguns bancos de dados, o bloqueio de uma linha também pode bloquear outras linhas.  
  
 Com o aumento do isolamento das transações vem a *concorrência reduzida,* ou a capacidade de duas transações de usar os mesmos dados ao mesmo tempo. Para obter mais informações, consulte [Configuração do nível de isolamento da transação](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Transações em ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Isolamento de transação](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Controle de Concorrência](../../../odbc/reference/develop-app/concurrency-control.md)
