---
title: Propriedade index | Microsoft Docs
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
ms.openlocfilehash: ba871d6d0e84b8068cb36a3ed2516a2665db28d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932432"
---
# <a name="index-property"></a>Propriedade Index
Indica o nome do índice atualmente em vigor para um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** , que é o nome do índice.  
  
## <a name="remarks"></a>Comentários  
 O índice nomeado pela propriedade **index** deve ter sido declarado anteriormente na tabela base subjacente ao objeto **Recordset** . Ou seja, o índice deve ter sido declarado programaticamente como um objeto de [índice](../../../ado/reference/adox-api/index-object-adox.md) ADOX ou quando a tabela base foi criada.  
  
 Ocorrerá um erro de tempo de execução se não for possível definir o índice. A propriedade **index** não pode ser definida nas seguintes condições:  
  
-   Dentro de um manipulador de eventos [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) ou **RecordsetChangeComplete** .  
  
-   Se o **conjunto de registros** ainda estiver executando uma operação (que pode ser determinada pela propriedade [State](../../../ado/reference/ado-api/state-property-ado.md) ).  
  
-   Se um filtro tiver sido definido no **conjunto de registros** com a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) .  
  
 A propriedade **index** sempre poderá ser definida com êxito se o **conjunto de registros** estiver fechado, mas o **conjunto de registros** não será aberto com êxito ou o índice não poderá ser usado se o provedor subjacente não oferecer suporte a índices.  
  
 Se o índice puder ser definido, a posição da linha atual poderá ser alterada. Isso causará uma atualização para a propriedade [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e acionará os eventos **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)e [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) .  
  
 Se o índice puder ser definido e a propriedade [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) for **adLockPessimistic** ou **adLockOptimistic**, uma operação [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) implícita será executada. Isso libera os grupos atuais e afetados. Qualquer filtro existente é liberado e a posição da linha atual é alterada para a primeira linha do **conjunto de registros**reordenado.  
  
 A propriedade **index** é usada em conjunto com o método [Seek](../../../ado/reference/ado-api/seek-method.md) . Se o provedor subjacente não oferecer suporte à propriedade **index** e, portanto, o método **Seek** , considere usar o método [Find](../../../ado/reference/ado-api/find-method-ado.md) em vez disso. Determine se o objeto **Recordset** dá suporte a índices com o método de [suporte](../../../ado/reference/ado-api/supports-method.md)**(adIndex)** .  
  
 A propriedade de **índice** interna não está relacionada à propriedade de [otimização](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dinâmica, embora ambas lidam com índices.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Seek e da propriedade index (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Método Seek](../../../ado/reference/ado-api/seek-method.md)
