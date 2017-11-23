---
title: "Serialização | Microsoft Docs"
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
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24abc4dee066853da7b201f19839063aa437d854
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="serializability"></a>Serialização
Idealmente, as transações devem ser *serializável*. As transações são consideradas serializável se os resultados da execução simultânea de transações são os mesmos que os resultados de executá-los em série — ou seja, um após o outro. Não é importante que transação executa pela primeira vez, apenas que o resultado não reflete qualquer combinação das transações.  
  
 Por exemplo, suponha que a transação A multiplica os valores de dados por 2 e a transação B adiciona 1 aos valores de dados. Agora suponha que há dois valores de dados: 0 e 10. Se essas transações são executadas um após o outro, os novos valores será 22 e 1 e 21 se a transação A for executada pela primeira vez, ou 2, se a transação B é executada primeiro. Mas e se a ordem na qual as duas transações são executadas é diferente para cada valor? Se a transação A é executada primeira no valor da primeira e a transação B são executados primeiro no segundo valor, os novos valores são 1 e 22. Se essa ordem é revertida, os novos valores são 2 e 21. As transações são serializáveis se 1, 21 e 2, 22 são os resultados só é possíveis. As transações não são serializável se 1, 22 ou 2, 21 é um resultado possíveis.  
  
 Então por que é serialização desejável? Em outras palavras, por que é importante que parece uma transação for concluída antes do início da próxima transação? Considere o seguinte problema. Um vendedor está inserindo pedidos ao mesmo tempo que envia um administrador de cobranças. Suponha que o vendedor entra em uma ordem de empresa X, mas não confirmada. o vendedor ainda está se comunicando com o representante da empresa X. O administrador solicita uma lista de todos os pedidos e descobre a ordem para a empresa X e envia uma fatura. Agora o representante da empresa X decide que deseja alterar a ordem para que o vendedor altera antes de confirmar a transação. Empresa X obtém uma fatura incorreta.  
  
 Se do vendedor e do administrador de transações fossem serializáveis, esse problema nunca ter ocorrido. A transação do vendedor deve terminar antes do início de transação do auxiliar, caso em que o administrador será ter enviado o bill correto ou transação do auxiliar deve terminar antes do início de transação do vendedor, caso em que o administrador não terá enviado uma fatura para a empresa X em todos os.
