---
title: Transições de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2512d277980b071523cfea6cbe132f2a3861b7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107296"
---
# <a name="state-transitions"></a>Transições de estado
O ODBC define *Estados* discretos para cada ambiente, cada conexão e cada instrução. Por exemplo, o ambiente tem três estados possíveis: não alocado (em que nenhum ambiente é alocado), alocado (no qual um ambiente é alocado, mas nenhuma conexão é alocada) e conexão (em que um ambiente e uma ou mais conexões são alocado). As conexões têm sete Estados possíveis; as instruções têm 13 estados possíveis.  
  
 Um item específico, conforme identificado por seu identificador, passa de um estado para outro quando o aplicativo chama uma determinada função ou funções e passa o identificador para esse item. Essa movimentação é chamada de *transição de estado*. Por exemplo, alocar um identificador de ambiente com **SQLAllocHandle** move o ambiente de não alocado para alocado e liberar esse identificador com **SQLFreeHandle** o retorna de alocado para não alocado. O ODBC define um número limitado de transições de estado legal, que é outra maneira de dizer que as funções devem ser chamadas em uma determinada ordem.  
  
 Algumas funções, como **SQLGetConnectAttr**, não afetam o estado. Outras funções afetam o estado de um único item. Por exemplo, **SQLDisconnect** move uma conexão de um estado de conexão para um estado alocado. Por fim, algumas funções afetam o estado de mais de um item. Por exemplo, alocar um identificador de conexão com o **SQLAllocHandle** move uma conexão de um estado não alocado para um de alocação e move o ambiente de um alocado para um estado de conexão.  
  
 Se um aplicativo chamar uma função fora de ordem, a função retornará um *erro de transição de estado*. Por exemplo, se um ambiente estiver em um estado de conexão e o aplicativo chamar **SQLFreeHandle** com esse identificador de ambiente, **SQLFREEHANDLE** retornará SQLSTATE HY010 (erro de sequência de função), pois ele só poderá ser chamado quando o ambiente estiver em um estado alocado. Ao definir isso como uma transição de estado inválida, o ODBC impede que o aplicativo libere o ambiente enquanto houver conexões ativas.  
  
 Algumas transições de estado são inerentes ao design do ODBC. Por exemplo, não é possível alocar um identificador de conexão sem primeiro alocar um identificador de ambiente, porque a função que aloca um identificador de conexão requer um identificador de ambiente. Outras transições de estado são impostas pelo Gerenciador de driver e pelos drivers. Por exemplo, **SQLExecute** executa uma instrução preparada. Se o identificador de instrução passado para ele não estiver em um estado preparado, **SQLExecute** retornará SQLSTATE HY010 (erro de sequência de função).  
  
 Do ponto de vista do aplicativo, as transições de Estado costumam ser simples: as transições de estado legais tendem a ficar em mãos com o fluxo de um aplicativo bem escrito. As transições de estado são mais complexas para o Gerenciador de driver e os drivers porque eles devem controlar o estado do ambiente, cada conexão e cada instrução. A maior parte desse trabalho é feita pelo Gerenciador de driver; a maior parte do trabalho que deve ser feito por drivers ocorre com instruções com resultados pendentes.  
  
 As partes 1 e 2 deste manual ("introdução ao ODBC" e "desenvolvimento de aplicativos e drivers") tendem a não mencionar explicitamente as transições de estado. Em vez disso, eles descrevem a ordem na qual as funções devem ser chamadas. Por exemplo, "Executing Statements" afirma que uma instrução deve ser preparada com **SQLPrepare** antes que possa ser executada com **SQLExecute**. Para obter uma descrição completa dos Estados e das transições de estado, incluindo quais transições são verificadas pelo Gerenciador de driver e quais devem ser verificadas por drivers, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
