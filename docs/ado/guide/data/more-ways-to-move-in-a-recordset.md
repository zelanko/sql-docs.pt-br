---
description: Mais maneiras de se mover em um conjunto de registros
title: Mais maneiras de se mover em um conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e8c668bc24b388d0367429086416cd67b5355550
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980287"
---
# <a name="more-ways-to-move-in-a-recordset"></a>Mais maneiras de se mover em um conjunto de registros
Os quatro métodos a seguir são usados para mover-se, ou rolar, no **conjunto de registros**: [MoveFirst, MoveLast, MoveNext e MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Alguns desses métodos não estão disponíveis em cursores de somente avanço.)  
  
 O **MoveFirst** altera a posição do registro atual para o primeiro registro no **conjunto de registros**. **MoveLast** altera a posição do registro atual para o último registro no **conjunto de registros**. Para usar o **MoveFirst** ou **MoveLast**, o objeto **Recordset** deve dar suporte a indicadores ou movimento de cursor para trás; caso contrário, a chamada do método gerará um erro.  
  
 **MoveNext** move a posição do registro atual um lugar para frente. Se você estiver no último registro quando chamar **MoveNext**, **EOF** será definido como **true**. **MovePrevious** move a posição do registro atual um local para trás. Se você estiver no primeiro registro quando chamar **MovePrevious**, **BOF** será definido como **true**. É recomendável verificar as propriedades **EOF** e **BOF** ao usar esses métodos e mover o cursor de volta para uma posição de registro atual válida se você sair de qualquer uma das extremidades do **conjunto de registros**, como mostrado aqui:  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 Ou, no caso do método **MovePrevious** :  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 Nos casos em que o **conjunto de registros** foi filtrado ou classificado e os dados do registro atual são alterados, a posição também pode ser alterada. Nesses casos, o método **MoveNext** funciona normalmente, mas lembre-se de que a posição é movida um registro para frente da nova posição, não da posição antiga. Por exemplo, alterar os dados no registro atual, de modo que o registro seja movido para o final do conjunto de **registros**classificado, significa que chamar **MoveNext** Results no ADO Configurando o registro atual para a posição após o último registro no **conjunto de registros** (**EOF**  =  **true**).  
  
 O comportamento dos vários métodos move do objeto **Recordset** depende, em certo ponto, dos dados dentro do **conjunto de registros**. Novos registros adicionados ao **conjunto de registros** são inicialmente adicionados em uma determinada ordem, que é definida pela fonte de dados e pode ser dependente implícita ou explicitamente nos dados no novo registro. Por exemplo, se uma classificação ou uma junção for feita dentro da consulta que popula o **conjunto de registros**, o novo registro será inserido no local apropriado dentro do **conjunto de registros**. Se a ordenação não for especificada explicitamente ao criar o **conjunto de registros**, as alterações na implementação da fonte de dados poderão fazer com que a ordem das linhas retornadas seja alterada inadvertidamente. Além disso, as funções de classificação, filtragem e edição do **conjunto de registros** podem afetar a ordem e, possivelmente, quais linhas no conjunto de registros estarão visíveis.  
  
 Portanto, **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**e **move** são todos sensíveis a outras operações executadas no mesmo **conjunto de registros**. O ADO sempre tentará manter sua posição atual até que você a mova explicitamente, mas, às vezes, as alterações intervenientes dificultam a compreensão dos efeitos de uma movimentação subsequente. Por exemplo, se você chamar **MoveFirst** para posição na primeira linha de um conjunto de **registros** classificado e alterar a classificação de ordem crescente para ordem decrescente, ainda estará na mesma linha, mas agora é a última linha do **conjunto de registros**. O **MoveFirst** levará você para uma linha diferente (a nova primeira linha).  
  
 Como outro exemplo, se você estiver posicionado em uma linha específica no meio de um **conjunto de registros** e chamar **delete** e, em seguida, chamar **MoveNext**, agora você estará no registro imediatamente após o registro excluído. Mas chamar **MovePrevious** torna o registro anterior ao que você excluiu o registro atual, pois o registro excluído não é mais contado na associação ativa do **conjunto de registros**.  
  
 É particularmente difícil definir a semântica de movimentação consistente em todos os provedores para métodos que se movem em relação ao registro atual – **MovePrevious**, **MoveNext**e **move** -in a face da alteração de dados no registro atual. Por exemplo, se você estiver trabalhando com um **conjunto de registros**filtrado e classificado e alterar os dados no registro atual para que ele precedesse todos os outros registros, mas os dados alterados também não corresponderem ao filtro, não será claro onde uma operação **MoveNext** deve levá-lo. A conclusão mais segura é que a movimentação relativa em um **conjunto de registros** é mais arriscada que a movimentação absoluta (como usar o **MoveFirst** ou **MoveLast**) quando os dados são alterados enquanto os registros estão sendo editados, adicionados ou excluídos. A classificação e a filtragem devem ser baseadas em uma chave primária ou ID, pois esse tipo de valor não deve ser alterado.