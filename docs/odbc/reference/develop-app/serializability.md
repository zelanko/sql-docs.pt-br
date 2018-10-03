---
title: Serialização | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93f138988e0b01d6408a7aec96d09ceff65a6f5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757714"
---
# <a name="serializability"></a>Seriabilidade
Idealmente, as transações devem ser *serializável*. As transações devem ser serializáveis se os resultados da execução simultânea de transações são os mesmos que os resultados da execução em série — ou seja, um após o outro. Não é importante saber qual transação executa primeiro, apenas que o resultado não reflete qualquer combinação das transações.  
  
 Por exemplo, suponha que a transação A multiplica os valores de dados por 2 e a transação B adiciona 1 aos valores de dados. Agora vamos supor que há dois valores de dados: 0 e 10. Se essas transações são executadas uma após a outra, os novos valores será 1 e se a transação A for executada pela primeira vez, de 21 e 22 ou 2 se a transação B é executada primeira. Mas e se a ordem na qual as duas transações são executadas é diferente para cada valor? Se um é executado primeiro no primeiro valor de transação e a transação B são executados primeiros no segundo valor, os novos valores são 1 e 22. Se essa ordem é invertida, os novos valores são 2 e 21. As transações são serializáveis se 1, 21 e 2, 22 são os resultados só é possíveis. As transações não são serializável se 1, 22 ou 2, 21 é um resultado possível.  
  
 Então, por que é capacidade de serialização desejável? Em outras palavras, por que é importante que ela seja exibida que uma transação for concluída antes do início da próxima transação? Considere o seguinte problema. Um Viajante é inserir pedidos ao mesmo tempo em que um administrador está enviando faturas. Suponha que o vendedor entra em uma ordem da empresa X, mas não confirma a ele; o vendedor ainda está se comunicando com o representante da empresa X. O administrador solicita uma lista de todos os pedidos e descobre a ordem para a empresa X e as envia uma fatura. Agora que o representante da empresa X decide que deseja alterar sua ordem, então o Viajante altera-la antes de confirmar a transação. Empresa X obtém uma fatura incorreta.  
  
 Se do vendedor e do auxiliar transações serializáveis, esse problema nunca teria ocorrido. Transação do vendedor seria terminar antes de iniciar transação do auxiliar, caso em que o administrador teria enviado fora da lista correta tanto a transação do auxiliar seria terminar antes de iniciar transação do vendedor, caso em que o administrador teria não enviado uma fatura para a empresa X em todos os.
