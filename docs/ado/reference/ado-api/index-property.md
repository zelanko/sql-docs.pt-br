---
title: Propriedade Index | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4194cf7bea9d2a7cb52ea255ee7a858cdf4de6e5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027968"
---
# <a name="index-property"></a>Propriedade Index
Indica o nome do índice atualmente em vigor para um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor, que é o nome do índice.  
  
## <a name="remarks"></a>Comentários  
 O índice nomeado pelos **índice** propriedade deve ter sido declarada anteriormente na tabela base subjacente a **Recordset** objeto. Ou seja, o índice deve ter sido declarado por meio de programação como um ADOX [índice](../../../ado/reference/adox-api/index-object-adox.md) objeto, ou quando a tabela base foi criada.  
  
 Se o índice não pode ser definido, ocorrerá um erro de tempo de execução. O **índice** propriedade não pode ser definida nas seguintes condições:  
  
-   Dentro de um [eventos WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) ou **RecordsetChangeComplete** manipulador de eventos.  
  
-   Se o **conjunto de registros** ainda está executando uma operação (que pode ser determinado com a [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade).  
  
-   Se um filtro tiver sido definido na **conjunto de registros** com o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade.  
  
 O **índice** propriedade sempre pode ser definida com êxito se o **conjunto de registros** for fechada, mas o **Recordset** não será aberto com êxito, ou o índice não será utilizável, se a provedor subjacente não oferece suporte a índices.  
  
 Se o índice pode ser definido, pode alterar a posição da linha atual. Isso fará com que uma atualização para o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propriedade e será acionado a **eventos WillChangeRecordset**, **RecordsetChangeComplete**, [eventos WillMove ](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), e [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) eventos.  
  
 Se o índice pode ser definido e o [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) é de propriedade **adLockPessimistic** ou **adLockOptimistic**, em seguida, implícito [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) operação é executada. Isso libera os grupos afetados e atuais. Qualquer filtro existente é liberado, e a posição da linha atual é alterada para a primeira linha da reordenados **conjunto de registros**.  
  
 O **índice** propriedade é usada em conjunto com o [busca](../../../ado/reference/ado-api/seek-method.md) método. Se o provedor subjacente não dá suporte a **índice** propriedade e, portanto, o **busca** método, considere o uso a [localizar](../../../ado/reference/ado-api/find-method-ado.md) método em vez disso. Determinar se o **conjunto de registros** objeto dá suporte a índices com o [suporta](../../../ado/reference/ado-api/supports-method.md)**(adIndex)** método.  
  
 Interna **índice** propriedade não está relacionada a dinâmica [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedade, embora ambos lidam com índices.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Index (VB) e do método Seek](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Método Seek](../../../ado/reference/ado-api/seek-method.md)
