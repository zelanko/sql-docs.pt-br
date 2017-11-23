---
title: "Transições de estado | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0483bc53e02fa645c48200323ed4573105d37dd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="state-transitions"></a>Transições de estado
ODBC define discretos *estados* para cada ambiente, cada conexão e cada instrução. Por exemplo, o ambiente tem três estados possíveis: não alocado (em que nenhum ambiente é alocada), alocado (em que é alocado a um ambiente, mas nenhuma conexão é alocado) e Conexão (em que um ambiente e uma ou mais conexões estão alocados). As conexões têm sete estados possíveis; instruções ter 13 possíveis estados.  
  
 Um item específico, conforme identificado por seu identificador, move de um estado para outro quando o aplicativo chama uma determinada função ou funções e transmite o identificador para esse item. Essa movimentação é chamada um *transição de estado*. Por exemplo, ao alocar um identificador de ambiente com **SQLAllocHandle** move o ambiente de não alocado para alocado e liberando esse identificador com **SQLFreeHandle** retorna de alocado para Não alocado. ODBC define um número limitado de transições de estado legal, que é outra maneira de dizer que funções devem ser chamadas em uma determinada ordem.  
  
 Algumas funções, como **SQLGetConnectAttr**, não afetam estado. Outras funções afetam o estado de um único item. Por exemplo, **SQLDisconnect** move uma conexão de um estado de Conexão para um estado alocado. Finalmente, algumas funções afetam o estado de mais de um item. Por exemplo, ao alocar um identificador de conexão com **SQLAllocHandle** move uma conexão de um não alocado para um estado alocado e mudar o ambiente de um alocado para um estado de Conexão.  
  
 Se um aplicativo chama uma função fora de ordem, a função retorna um *erro de transição de estado*. Por exemplo, se um ambiente está em um estado de Conexão e o aplicativo chama **SQLFreeHandle** com esse identificador de ambiente, **SQLFreeHandle** retorna SQLSTATE HY010 (erro de sequência de função), porque ele pode ser chamado apenas quando o ambiente está em um estado alocado. Ao definir isso como uma transição de estado inválido, ODBC, impede que o aplicativo libera o ambiente enquanto houver conexões ativas.  
  
 Algumas transições de estado são inerentes no design do ODBC. Por exemplo, não é possível alocar um identificador de conexão sem primeiro alocar um identificador de ambiente, porque a função que aloca um identificador de conexão exige um identificador de ambiente. Outras transições de estado são impostas pelo Gerenciador de Driver e os drivers. Por exemplo, **SQLExecute** executa uma instrução preparada. Se o identificador de instrução passado para não é em um estado preparado, **SQLExecute** retornará SQLSTATE HY010 (erro de sequência de função).  
  
 Do ponto de vista do aplicativo, as transições de estado são geralmente simples: transições de estado Legal tendem a ir lado a lado com o fluxo de um aplicativo bem escrito. Transições de estado são mais complexas para o Gerenciador de Driver e os drivers porque eles devem controlar o estado de cada instrução, cada conexão e o ambiente. A maior parte desse trabalho é feita pelo Gerenciador de Driver; a maioria do trabalho que deve ser feita por drivers ocorre com as instruções com resultados pendentes.  
  
 Partes de 1 e 2 deste manual ("Introdução ao ODBC" e "Desenvolvimento de aplicativos e Drivers") tendem a não mencione explicitamente as transições de estado. Em vez disso, eles descrevem a ordem na qual as funções devem ser chamadas. Por exemplo, "Executando instruções" indica que uma instrução deve ser preparada com **SQLPrepare** antes que ele pode ser executado com **SQLExecute**. Para obter uma descrição completa de estados e transições de estado, incluindo quais transições são verificadas pelo Gerenciador de Driver e que deve ser verificado por drivers, consulte [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
