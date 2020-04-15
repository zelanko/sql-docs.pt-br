---
title: Transições estaduais | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a480b7ff8953ef94f0efc4886a09731730a61b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299689"
---
# <a name="state-transitions"></a>Transições de estado
A ODBC define *estados* discretos para cada ambiente, cada conexão e cada declaração. Por exemplo, o ambiente tem três estados possíveis: Não alocado (no qual nenhum ambiente é alocado), Alocado (no qual um ambiente é alocado, mas nenhuma conexão é alocada) e Conexão (em que um ambiente e uma ou mais conexões são alocadas). As conexões têm sete estados possíveis; declarações têm 13 estados possíveis.  
  
 Um determinado item, identificado por sua alça, se move de um estado para outro quando o aplicativo chama uma determinada função ou funções e passa a alça para esse item. Tal movimento é chamado de *transição de Estado.* Por exemplo, alocar uma alça de ambiente com **o SQLAllocHandle** move o ambiente de Não Alocado para Alocado e a liberação dessa alça com **o SQLFreeHandle** o devolve de Alocado para Não Alocado. A ODBC define um número limitado de transições legais de Estado, que é outra maneira de dizer que as funções devem ser chamadas em uma determinada ordem.  
  
 Algumas funções, como **SQLGetConnectAttr,** não afetam em nada o estado. Outras funções afetam o estado de um único item. Por exemplo, **o SQLDisconnect** move uma conexão de um estado de conexão para um estado alocado. Finalmente, algumas funções afetam o estado de mais de um item. Por exemplo, alocar uma alça de conexão com **o SQLAllocHandle** move uma conexão de um estado não alocado para um estado alocado e move o ambiente de um estado alocado para um estado de conexão.  
  
 Se um aplicativo chamar uma função fora de ordem, a função retorna um *erro de transição de estado*. Por exemplo, se um ambiente estiver em um estado de conexão e o aplicativo chamar **SQLFreeHandle** com essa alça de ambiente, **o SQLFreeHandle** retorna SQLSTATE HY010 (erro de seqüência de função), porque ele só pode ser chamado quando o ambiente está em um estado alocado. Ao defini-lo como uma transição de estado inválida, o ODBC impede que a aplicação liberte o ambiente enquanto houver conexões ativas.  
  
 Algumas transições de estado são inerentes ao projeto da ODBC. Por exemplo, não é possível alocar uma alça de conexão sem antes alocar uma alça de ambiente, porque a função que aloca uma alça de conexão requer uma alça do ambiente. Outras transições estaduais são impostas pelo Driver Manager e pelos motoristas. Por exemplo, **o SQLExecute** executa uma declaração preparada. Se a alça da declaração passar para ela não estiver em um estado preparado, **o SQLExecute** retorna SQLSTATE HY010 (erro de seqüência de função).  
  
 Do ponto de vista do aplicativo, as transições de estado geralmente são simples: as transições de estado legal tendem a ir lado a lado com o fluxo de uma aplicação bem escrita. As transições estaduais são mais complexas para o Driver Manager e os drivers porque devem acompanhar o estado do ambiente, cada conexão e cada declaração. A maior parte deste trabalho é feito pelo Driver Manager; a maior parte do trabalho que deve ser feito pelos motoristas ocorre com declarações com resultados pendentes.  
  
 As partes 1 e 2 deste manual ("Introdução ao ODBC" e "Aplicativos e Drivers em desenvolvimento") tendem a não mencionar explicitamente as transições de estado. Em vez disso, descrevem a ordem em que as funções devem ser chamadas. Por exemplo, "Executando declarações" afirma que uma instrução deve ser preparada com **o SQLPrepare** antes de ser executada com **o SQLExecute**. Para obter uma descrição completa das transições de estados e estados, incluindo quais transições são verificadas pelo Driver Manager e que devem ser verificadas pelos motoristas, consulte [o apêndice B: Tabelas de Transição estaduais oDBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
