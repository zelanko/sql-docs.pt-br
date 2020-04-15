---
title: Serializabilidade | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0557e011578d313765614c05a2a9cf1b975bbc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304157"
---
# <a name="serializability"></a>Seriabilidade
Idealmente, as transações devem ser *serializáveis*. Dizem que as transações são serializáveis se os resultados da execução de transações simultaneamente forem os mesmos que os resultados de executá-las em série - ou seja, um após o outro. Não é importante qual transação executa primeiro, apenas que o resultado não reflita qualquer mistura das transações.  
  
 Por exemplo, suponha que a transação A multiplique valores de dados por 2 e a transação B adicione 1 aos valores de dados. Agora suponha que existam dois valores de dados: 0 e 10. Se essas transações forem executadas uma após a outra, os novos valores serão 1 e 21 se a transação A for executada primeiro, ou 2 e 22 se a transação B for executada primeiro. Mas e se a ordem em que as duas transações são executadas for diferente para cada valor? Se a transação A for executada primeiro no primeiro valor e a transação B for executada primeiro no segundo valor, os novos valores serão 1 e 22. Se essa ordem for invertida, os novos valores serão 2 e 21. As transações são serializáveis se 1, 21 e 2, 22 forem os únicos resultados possíveis. As transações não são serializáveis se 1, 22 ou 2, 21 for um resultado possível.  
  
 Então por que a serializabilidade é desejável? Em outras palavras, por que é importante que uma transação termine antes do início da próxima transação? Considere o seguinte problema. Um vendedor está enviando pedidos ao mesmo tempo que um funcionário está enviando contas. Suponha que o vendedor digite um pedido da Empresa X, mas não o cometa; o vendedor ainda está falando com o representante da Empresa X. O funcionário solicita uma lista de todos os pedidos abertos e descobre o pedido para a Empresa X e envia-lhes uma conta. Agora, o representante da Empresa X decide que quer mudar seu pedido, então o vendedor muda antes de cometer a transação. A Empresa X recebe uma nota incorreta.  
  
 Se as transações do vendedor e do balconista fossem serializáveis, esse problema nunca teria ocorrido. Ou a transação do vendedor teria terminado antes do início da transação do balconista, nesse caso o funcionário teria enviado a conta correta, ou a transação do balconista teria terminado antes do início da transação do vendedor, nesse caso o funcionário não teria enviado uma conta para a Empresa X.
