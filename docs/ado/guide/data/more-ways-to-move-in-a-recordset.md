---
title: Outras maneiras de mover em um conjunto de registros | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3e3f666fd96a1b00d78ba364a8df062fa3f6397
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="more-ways-to-move-in-a-recordset"></a>Outras maneiras de mover em um conjunto de registros
Os quatro métodos a seguir são usados para mover ou role, o **registros**: [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Alguns desses métodos estão disponíveis nos cursores de somente avanço.)  
  
 **MoveFirst** altera a posição do registro atual para o primeiro registro de **registros**. **MoveLast** altera o registro atual para a última posição o registro no **registros**. Para usar **MoveFirst** ou **MoveLast**, o **registros** objeto deve dar suporte a indicadores ou movimento do cursor com versões anteriores; caso contrário, a chamada do método gerará um erro.  
  
 **MoveNext** move o registro atual posicionar um lugar para frente. Se você estiver usando o último registro quando você chama **MoveNext**, **EOF** será definida como **True**. **MovePrevious** move o registro atual posicionar um só lugar com versões anteriores. Se você está no primeiro registro quando você chamar **MovePrevious**, **BOF** será definida como **True**. É recomendável verificar o **EOF** e **BOF** propriedades ao usar esses métodos e para mover o cursor de volta para uma posição válida de registro atual se você sair da extremidade do **registros**, conforme mostrado aqui:  
  
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
  
 Em casos onde o **registros** filtrado ou classificado e dados do registro atual são alterados, também pode alterar a posição. Nesses casos o **MoveNext** método funciona normalmente, mas lembre-se de que a posição seja movido para frente gravar a nova posição, não a antiga posição. Por exemplo, alterar os dados no registro atual, de modo que o registro é movido para o final do classificada **registros**, significa que a chamada **MoveNext** resulta em ADO definindo o registro atual o posição após o último registro de **registros** (**EOF** = **True**).  
  
 O comportamento dos vários métodos de movimentação do **conjunto de registros** depende do objeto, até certo ponto, os dados dentro de **conjunto de registros**. Novos registros adicionados para o **registros** inicialmente são adicionados em uma ordem específica, que é definida pela fonte de dados e pode ser dependente implicitamente ou explicitamente nos dados no novo registro. Por exemplo, se uma classificação ou um associação é feita dentro de uma consulta que preenche a **Recordset**, o novo registro será inserido no local apropriado dentro a **registros**. Se a classificação não for especificado explicitamente ao criar o **Recordset**, as alterações na implementação de fonte de dados podem fazer com que a ordem das linhas retornadas alterar inadvertidamente. Além disso, a classificação, filtragem e editar funções do **registros** podem afetar a ordem e possivelmente quais linhas no conjunto de registros serão visíveis.  
  
 Portanto, **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, e **mover** são todos sensível a outras operações executadas na mesma **registros**. ADO sempre tentará manter sua posição atual até que você explicitamente movê-la, mas às vezes, as alterações intermediárias dificultam a entender os efeitos de uma movimentação subsequente. Por exemplo, se você chamar **MoveFirst** a posição na primeira linha de um classificada **registros** e você alterar a classificação de ordem crescente para decrescente, você ainda estiverem na mesma linha —, mas agora ela é a última linha no **registros**. **MoveFirst** levará para uma linha diferente (a nova linha primeiro).  
  
 Como outro exemplo, se você está posicionado em uma linha específica no meio de um **registros** e você chamar **excluir** e, em seguida, chame **MoveNext**, agora você está no registro imediatamente após o registro excluído. Mas chamada **MovePrevious** faz com que o registro anterior aquele que você excluiu o registro atual, porque o registro excluído não é contado na associação de ativos do **registros**.  
  
 É muito difícil definir semânticas de movimentação consistente em todos os provedores para métodos que se movem em relação ao registro atual — **MovePrevious**, **MoveNext**, e **mover** — no caso de alteração de dados no registro atual. Por exemplo, se você estiver trabalhando com um classificados, filtrados **registros**e você alterar os dados no registro atual para que ele deve preceder todos os outros registros, mas os dados alterados também não correspondem ao filtro, não está claro onde um **MoveNext** operação deve levar você. Concluir a mais segura é essa movimentação relativa dentro de um **Recordset** é mais arriscados que absoluto movimento (como o uso de **MoveFirst** ou **MoveLast**) quando os dados são a alteração enquanto os registros estão sendo editados, adicionadas ou excluídas. Classificação e filtragem devem ser baseados em uma chave primária ou a ID, porque esse tipo de valor não deve ser alterada.

