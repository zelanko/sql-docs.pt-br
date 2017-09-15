---
title: Propriedade UnderlyingValue | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4699695a6a74c5da7dca4445c35d605cd399795d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="underlyingvalue-property"></a>Propriedade UnderlyingValue
Indica o valor atual de um [campo](../../../ado/reference/ado-api/field-object.md) objeto no banco de dados.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **Variant** valor que indica o valor de **campo**.  
  
## <a name="remarks"></a>Comentários  
 Use o **UnderlyingValue** propriedade para retornar o valor do campo atual do banco de dados. O valor do campo no **UnderlyingValue** propriedade é o valor que é visível para a transação e pode ser o resultado de uma atualização recente por outra transação. Isso pode ser diferente do [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) propriedade, que reflete o valor que foi originalmente retornado para o [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Isso é semelhante a usar o [Resync](../../../ado/reference/ado-api/resync-method.md) método, mas o **UnderlyingValue** propriedade retorna apenas o valor de um determinado campo do registro atual. Esse é o mesmo valor que o [Resync](../../../ado/reference/ado-api/resync-method.md) usa o método para substituir o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade.  
  
 Quando você usa essa propriedade com o **OriginalValue** propriedade, você pode resolver conflitos que podem surgir de atualizações em lotes.  
  
## <a name="record"></a>Record  
 Para [registro](../../../ado/reference/ado-api/record-object-ado.md) objetos, essa propriedade será vazia para campos adicionados antes [atualização](../../../ado/reference/ado-api/update-method.md) é chamado.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de UnderlyingValue (VB) e OriginalValue](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Exemplo de propriedades de UnderlyingValue (VC + +) e OriginalValue](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propriedade OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)

