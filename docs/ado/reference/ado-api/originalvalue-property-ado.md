---
title: Propriedade OriginalValue (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 512569ce2baa8acabdf8bcbf8f637ebf20e4f613
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917841"
---
# <a name="originalvalue-property-ado"></a>Propriedade OriginalValue (ADO)
Indica o valor de um [campo](../../../ado/reference/ado-api/field-object.md) que existia no registro antes de qualquer alteração ser feita.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor **Variant** que representa o valor de um campo antes de qualquer alteração.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **OriginalValue** para retornar o valor do campo original para um campo do registro atual.  
  
 No *modo de atualização imediata* (no qual o provedor grava alterações na fonte de dados subjacente depois que você chama o método [Update](../../../ado/reference/ado-api/update-method.md) ), a propriedade **OriginalValue** retorna o valor do campo que existia antes de qualquer alteração (isto é, desde a última chamada do método **Update** ). Esse é o mesmo valor que o método [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) usa para substituir a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) .  
  
 No *modo de atualização em lotes* (no qual o provedor armazena em cache várias alterações e as grava na fonte de dados subjacente somente quando você chama o método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) ), a propriedade **OriginalValue** retorna o valor do campo que existia antes de qualquer alteração (ou seja, desde a última chamada do método **UpdateBatch** ). Esse é o mesmo valor que o método [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) usa para substituir a propriedade **Value** . Ao usar essa propriedade com a propriedade [subdependent](../../../ado/reference/ado-api/underlyingvalue-property.md) , você pode resolver conflitos que surgem de atualizações em lotes.  
  
## <a name="record"></a>Record  
 Para objetos de [registro](../../../ado/reference/ado-api/record-object-ado.md) , a propriedade **OriginalValue** estará vazia para os campos adicionados antes de a [atualização](../../../ado/reference/ado-api/update-method.md) ser chamada.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades OriginalValue e subdependvalue (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Exemplo das propriedades OriginalValue e subdependvalue (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propriedade UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
