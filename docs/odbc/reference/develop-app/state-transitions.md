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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107296"
---
# <a name="state-transitions"></a>Transições de estado
ODBC define discreto *estados* para cada ambiente, cada conexão e cada instrução. Por exemplo, o ambiente tem três estados possíveis: Não alocado (em que nenhum ambiente é alocado), alocado (em que um ambiente é alocado, mas nenhuma conexão é alocado) e Conexão (em que um ambiente e uma ou mais conexões estão alocadas). As conexões têm sete estados possíveis; as instruções ter 13 estados possíveis.  
  
 Um item específico, conforme identificado por seu identificador, move de um estado para outro quando o aplicativo chama uma determinada função ou funções e transmite o identificador para esse item. Essa movimentação é chamada de um *transição de estado*. Por exemplo, alocando um identificador de ambiente com **SQLAllocHandle** move o ambiente de não alocado para alocado e liberando esse identificador com **SQLFreeHandle** retorna-o de alocado para Não alocado. ODBC define um número limitado de transições de estado legal, que é outra maneira de dizer que as funções devem ser chamadas em uma determinada ordem.  
  
 Algumas funções, como **SQLGetConnectAttr**, não afetam estado. Outras funções afetam o estado de um único item. Por exemplo, **SQLDisconnect** move uma conexão de um estado de Conexão para um estado alocado. Por fim, algumas funções afetam o estado de mais de um item. Por exemplo, alocando um identificador de conexão com **SQLAllocHandle** move uma conexão de um não alocado para um estado alocado e move o ambiente de um alocado para um estado de Conexão.  
  
 Se um aplicativo chama uma função fora de ordem, a função retorna um *erro de transição de estado*. Por exemplo, se um ambiente está em um estado de Conexão e o aplicativo chama **SQLFreeHandle** com esse identificador de ambiente **SQLFreeHandle** retornará SQLSTATE HY010 (erro de sequência de função), porque ele pode ser chamado somente quando o ambiente está em um estado alocado. Ao definir isso como uma transição de estado inválida, ODBC, impede que o aplicativo liberando o ambiente enquanto houver conexões ativas.  
  
 Alguns transições de estado são inerentes no design do ODBC. Por exemplo, não é possível alocar um identificador de conexão sem primeiro alocar um identificador de ambiente, pois a função que aloca um identificador de conexão exige um identificador de ambiente. Outras transições de estado são impostas pelo Gerenciador de Driver e os drivers. Por exemplo, **SQLExecute** executa uma instrução preparada. Se o identificador de instrução é passado para ele não está em um estado de preparada, **SQLExecute** retornará SQLSTATE HY010 (erro de sequência de função).  
  
 Do ponto de vista do aplicativo, as transições de estado são geralmente simples: Transições de estado legal tendem a mão de mãos dadas com o fluxo de um aplicativo bem escrito. Transições de estado são mais complexas para o Gerenciador de Driver e os drivers, porque eles devem controlar o estado de cada instrução, cada conexão e o ambiente. A maior parte desse trabalho é feita pelo Gerenciador de Driver; ocorre a maior parte do trabalho que deve ser feito por drivers com as instruções com resultados pendentes.  
  
 Partes de 1 e 2 deste manual ("Introdução ao ODBC" e "Desenvolvimento de aplicativos e Drivers") tendem a não mencione explicitamente as transições de estado. Em vez disso, eles descrevem a ordem na qual as funções devem ser chamadas. Por exemplo, "Executando instruções" indica que uma instrução deve ser preparada com **SQLPrepare** antes que ele pode ser executado com **SQLExecute**. Para obter uma descrição completa de estados e transições de estado, incluindo quais transições são verificadas pelo Gerenciador de Driver e que deve ser verificado por drivers, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
