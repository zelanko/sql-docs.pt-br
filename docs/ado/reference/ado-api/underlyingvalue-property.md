---
description: Propriedade UnderlyingValue
title: Propriedade subdependvalue | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a96924a682a0c916da8c6834ea7b290b88b6f690
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988167"
---
# <a name="underlyingvalue-property"></a>Propriedade UnderlyingValue
Indica o valor atual de um objeto de [campo](./field-object.md) no banco de dados.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **Variant** que indica o valor do **campo**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **subdependvalue** para retornar o valor do campo atual do banco de dados. O valor do campo na propriedade **subdependvalue** é o valor que é visível para sua transação e pode ser o resultado de uma atualização recente por outra transação. Isso pode ser diferente da propriedade [OriginalValue](./originalvalue-property-ado.md) , que reflete o valor retornado originalmente para o conjunto de [registros](./recordset-object-ado.md).  
  
 Isso é semelhante ao uso do método [Ressync](./resync-method.md) , mas a propriedade **subdependvalue** retorna apenas o valor de um campo específico do registro atual. Esse é o mesmo valor usado pelo método [Resync](./resync-method.md) para substituir a propriedade [Value](./value-property-ado.md) .  
  
 Ao usar essa propriedade com a propriedade **OriginalValue** , você pode resolver conflitos que surgem de atualizações em lotes.  
  
## <a name="record"></a>Record  
 Para objetos de [registro](./record-object-ado.md) , essa propriedade estará vazia para os campos adicionados antes da [atualização](./update-method.md) ser chamada.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](./field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades OriginalValue e subdependvalue (VB)](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Exemplo das propriedades OriginalValue e subdependvalue (VC + +)](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propriedade OriginalValue (ADO)](./originalvalue-property-ado.md)   
 [Método Resync](./resync-method.md)