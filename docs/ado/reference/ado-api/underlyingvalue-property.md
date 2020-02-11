---
title: Propriedade subdependvalue | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 582d0b87edd4729ce54cc2a7323b0a63443cab82
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938854"
---
# <a name="underlyingvalue-property"></a>Propriedade UnderlyingValue
Indica o valor atual de um objeto de [campo](../../../ado/reference/ado-api/field-object.md) no banco de dados.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor **Variant** que indica o valor do **campo**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **subdependvalue** para retornar o valor do campo atual do banco de dados. O valor do campo na propriedade **subdependvalue** é o valor que é visível para sua transação e pode ser o resultado de uma atualização recente por outra transação. Isso pode ser diferente da propriedade [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) , que reflete o valor retornado originalmente para o conjunto de [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Isso é semelhante ao uso do método [Ressync](../../../ado/reference/ado-api/resync-method.md) , mas a propriedade **subdependvalue** retorna apenas o valor de um campo específico do registro atual. Esse é o mesmo valor usado pelo método [Resync](../../../ado/reference/ado-api/resync-method.md) para substituir a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) .  
  
 Ao usar essa propriedade com a propriedade **OriginalValue** , você pode resolver conflitos que surgem de atualizações em lotes.  
  
## <a name="record"></a>Registro  
 Para objetos de [registro](../../../ado/reference/ado-api/record-object-ado.md) , essa propriedade estará vazia para os campos adicionados antes da [atualização](../../../ado/reference/ado-api/update-method.md) ser chamada.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades OriginalValue e subdependvalue (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Exemplo das propriedades OriginalValue e subdependvalue (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propriedade OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)
