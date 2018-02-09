---
title: Propriedade Index | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 441b310afc4465c21f84d4dfe67c6b5928cb5f42
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="index-property"></a>Propriedade Index
Indica o nome do índice atualmente em vigor para um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor, que é o nome do índice.  
  
## <a name="remarks"></a>Remarks  
 O índice nomeado pelo **índice** propriedade deve ter sido declarada anteriormente na tabela base subjacente a **registros** objeto. Ou seja, o índice deve ter sido declarado programaticamente como um ADOX [índice](../../../ado/reference/adox-api/index-object-adox.md) objeto, ou quando a tabela base foi criada.  
  
 Se o índice não pode ser definido, ocorrerá um erro de tempo de execução. O **índice** propriedade não pode ser definida nas seguintes condições:  
  
-   Dentro de um [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) ou **RecordsetChangeComplete** manipulador de eventos.  
  
-   Se o **registros** ainda está executando uma operação (que pode ser determinado pelo [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade).  
  
-   Se um filtro tiver sido definido no **registros** com o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade.  
  
 O **índice** propriedade sempre pode ser definida com êxito se o **Recordset** for fechada, mas o **Recordset** não será aberto com êxito, ou o índice não será utilizável, se a provedor subjacente não oferece suporte a índices.  
  
 Se o índice pode ser definido, pode alterar a posição da linha atual. Isso fará com que uma atualização para o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) propriedade e disparam o **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove ](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), e [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) eventos.  
  
 Se o índice pode ser definido e o [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) é de propriedade **adLockPessimistic** ou **adLockOptimistic**, em seguida, implícita [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) operação é executada. Isso libera os grupos afetados e atuais. Qualquer filtro existente é lançado e a posição da linha atual é alterada para a primeira linha do reordenada **registros**.  
  
 O **índice** propriedade é usada em conjunto com o [busca](../../../ado/reference/ado-api/seek-method.md) método. Se o provedor subjacente não oferece suporte a **índice** propriedade e, portanto, o **busca** método, considere usar o [localizar](../../../ado/reference/ado-api/find-method-ado.md) método em vez disso. Determinar se o **registros** objeto oferece suporte a índices com o [dá suporte a](../../../ado/reference/ado-api/supports-method.md)**(adIndex)** método.  
  
 O interno **índice** propriedade não está relacionada ao dinâmico [otimizar](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) propriedade, embora ambos lidem com índices.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade de índice (VB) e método de busca](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Objeto de índice (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Método Seek](../../../ado/reference/ado-api/seek-method.md)
