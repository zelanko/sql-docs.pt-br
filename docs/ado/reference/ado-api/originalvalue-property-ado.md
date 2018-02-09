---
title: Propriedade OriginalValue (ADO) | Microsoft Docs
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
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8cc3597b6f3b476a889f836ae899f558b38eff20
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="originalvalue-property-ado"></a>Propriedade OriginalValue (ADO)
Indica o valor de um [campo](../../../ado/reference/ado-api/field-object.md) que existiam no registro antes das alterações foram feitas.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **Variant** valor que representa o valor de um campo antes de qualquer alteração.  
  
## <a name="remarks"></a>Remarks  
 Use o **OriginalValue** propriedade para retornar o valor do campo original de um campo do registro atual.  
  
 Em *modo de atualização imediata* (no qual o provedor grava alterações para a fonte de dados depois de chamar o [atualizar](../../../ado/reference/ado-api/update-method.md) método), o **OriginalValue** retorna de propriedade o valor do campo que existiam antes das alterações (ou seja, desde a última **atualização** chamada de método). Esse é o mesmo valor que o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) usa o método para substituir o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade.  
  
 Em *o modo de atualização em lotes* (no qual o provedor armazena em cache várias alterações e grava a fonte de dados somente quando você chamar o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), o **OriginalValue** propriedade retorna o valor do campo que existiam antes das alterações (ou seja, desde a última **UpdateBatch** chamada de método). Esse é o mesmo valor que o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) usa o método para substituir o **valor** propriedade. Quando você usa essa propriedade com o [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) propriedade, você pode resolver conflitos que podem surgir de atualizações em lotes.  
  
## <a name="record"></a>Record  
 Para [registro](../../../ado/reference/ado-api/record-object-ado.md) objetos, o **OriginalValue** propriedade estará vazia para campos adicionados antes [atualização](../../../ado/reference/ado-api/update-method.md) é chamado.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de UnderlyingValue (VB) e OriginalValue](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Exemplo de propriedades de UnderlyingValue (VC + +) e OriginalValue](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propriedade UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
