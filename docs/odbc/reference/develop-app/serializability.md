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
ms.openlocfilehash: 49552e7333d8cac2b55a9ae6e8dd7a41ff4c5955
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094329"
---
# <a name="serializability"></a>Seriabilidade
O ideal é que as transações sejam *serializáveis*. As transações serão consideradas serializáveis se os resultados das transações em execução simultaneamente forem os mesmos que os resultados da execução serial, ou seja, um após o outro. Não é importante que a transação seja executada primeiro, apenas que o resultado não reflita nenhuma combinação das transações.  
  
 Por exemplo, suponha que A transação A multiplique valores de dados por 2 e a transação B adicione 1 a valores de dados. Agora suponha que haja dois valores de dados: 0 e 10. Se essas transações forem executadas uma após a outra, os novos valores serão 1 e 21 se a transação A for executada primeiro, ou 2 e 22 se A transação B for executada primeiro. Mas e se a ordem na qual as duas transações são executadas for diferente para cada valor? Se a transação A for executada primeiro no primeiro valor e a transação B for executada primeiro no segundo valor, os novos valores serão 1 e 22. Se esse pedido for revertido, os novos valores serão 2 e 21. As transações serão serializáveis se 1, 21 e 2, 22 forem os únicos resultados possíveis. As transações não serão serializáveis se 1, 22 ou 2, 21 for um resultado possível.  
  
 Então, por que o serialização é desejável? Em outras palavras, por que é importante que pareça que uma transação é concluída antes do início da próxima transação? Considere o seguinte problema. Um vendedor está inserindo pedidos ao mesmo tempo em que um administrador está enviando faturas. Suponha que o vendedor Insira um pedido da empresa X, mas não o confirme; o vendedor ainda está se comunicando com o representante da empresa X. O auxiliar solicita uma lista de todos os pedidos abertos e descobre a ordem da empresa X e envia uma conta. Agora, o representante da empresa X decide que deseja alterar sua ordem, de modo que o vendedor o altera antes de confirmar a transação. A empresa X Obtém uma fatura incorreta.  
  
 Se as transações do vendedor e do administrador fossem serializáveis, esse problema nunca ocorreu. A transação do vendedor teria terminado antes do início da transação do administrador, caso em que o administrador teria enviado a conta correta, ou a transação do administrador teria sido concluída antes da transação do vendedor ser iniciada; nesse caso, o o auxiliar não teria enviado uma fatura para a empresa X.
