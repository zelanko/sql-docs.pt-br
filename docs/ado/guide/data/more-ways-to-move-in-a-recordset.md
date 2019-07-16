---
title: Mais maneiras de mover em um conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ea83f40c6d6e595277a173c181c24f33e382393
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924884"
---
# <a name="more-ways-to-move-in-a-recordset"></a>Mais maneiras de se mover em um conjunto de registros
Os quatro métodos a seguir são usados para mover-se ou role, o **Recordset**: [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Alguns desses métodos estão disponíveis nos cursores de somente avanço.)  
  
 **MoveFirst** altera a posição do registro atual para o primeiro registro a **conjunto de registros**. **MoveLast** altera o registro atual para a última posição o registro em de **conjunto de registros**. Para usar **MoveFirst** ou **MoveLast**, o **Recordset** objeto deve dar suporte a indicadores ou movimento do cursor com versões anteriores; caso contrário, a chamada de método irá gerar um erro.  
  
 **MoveNext** move o registro atual posicionar um só lugar para frente. Se você estiver usando o último registro quando você chama **MoveNext**, **EOF** será definido como **verdadeiro**. **MovePrevious** move o registro atual posicionar um só lugar com versões anteriores. Se você está no primeiro registro quando você chama **MovePrevious**, **BOF** será definido como **verdadeiro**. É aconselhável verificar a **EOF** e **BOF** propriedades ao usar esses métodos e para mover o cursor de volta para uma posição do registro atual válida se você deixar de usar ambas as extremidades do **Recordset**, conforme mostrado aqui:  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 Ou, no caso do **MovePrevious** método:  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 Em casos em que o **Recordset** filtrada ou classificada e dados do registro atual são alterados, a posição também pode ser alteradas. Nesses casos, o **MoveNext** método normalmente funciona, mas lembre-se de que a posição é movida gravar a nova posição, não a antiga posição para frente. Por exemplo, alterar os dados no registro atual, de modo que o registro é movido para o final do classificado **conjunto de registros**, significa que a chamada **MoveNext** resulta em ADO, definindo o registro atual o posição após o último registro a **conjunto de registros** (**EOF** = **True**).  
  
 O comportamento dos vários métodos de movimentação do **conjunto de registros** depende do objeto, até certo ponto, nos dados dentro de **conjunto de registros**. Novos registros adicionados para o **Recordset** são adicionadas inicialmente em uma ordem específica, que é definida pela fonte de dados e pode ser dependente implicitamente ou explicitamente nos dados no novo registro. Por exemplo, se uma classificação ou uma junção é feita dentro da consulta que preenche o **conjunto de registros**, o novo registro será inserido no local apropriado dentro de **conjunto de registros**. Se a ordenação não for especificada explicitamente ao criar o **Recordset**, alterações na implementação do código-fonte de dados podem fazer com que a ordenação das linhas retornadas alterar inadvertidamente. Além disso, a classificação, filtragem e editar funções do **Recordset** pode afetar a ordem e, possivelmente, quais linhas no conjunto de registros estarão visíveis.  
  
 Portanto, **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, e **mover** são todos minúsculas para outras operações executadas na mesma **conjunto de registros**. ADO sempre tentará manter sua posição atual até que você explicitamente movê-lo, mas às vezes, as alterações intermediárias torná-lo difícil de entender os efeitos de uma troca subsequente. Por exemplo, se você chamar **MoveFirst** para a posição na primeira linha de um classificado **Recordset** e você altera a classificação de ordem crescente para decrescente, você ainda está na mesma linha, mas agora é a última linha no **conjunto de registros**. **MoveFirst** levará você até uma linha diferente (a nova linha primeiro).  
  
 Como outro exemplo, se você estiver localizado em uma determinada linha no meio de um **conjunto de registros** e chamar **excluir** e, em seguida, chame **MoveNext**, agora você está no registro imediatamente após o registro excluído. Mas a chamada **MovePrevious** faz com que o registro anterior aquele que você excluiu o registro atual, porque o registro excluído não é contado na associação do Active Directory a **conjunto de registros**.  
  
 Ele é especialmente difícil de definir a semântica de movimentação consistente em todos os provedores para os métodos que se movem em relação ao registro atual - **MovePrevious**, **MoveNext**, e **mover** - em caso de alteração de dados no registro atual. Por exemplo, se você estiver trabalhando com um classificado, filtrado **Recordset**e você alterar os dados no registro atual para que ele preceder todos os outros registros, mas os dados alterados também não coincide mais com o filtro, não fica claro onde um **MoveNext** operação deve levar você. A conclusão mais segura é essa movimentação relativa dentro de um **conjunto de registros** é mais arriscadas do que a movimentação absoluta (como o uso de **MoveFirst** ou **MoveLast**) quando os dados são a alteração enquanto os registros estão sendo editados, adicionadas ou excluídas. Classificação e filtragem devem ser baseados em uma chave primária ou a ID, porque esse tipo de valor não deve ser alterada.
