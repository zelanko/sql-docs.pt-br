---
description: Propriedade OriginalValue (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5aedfa688b2d29a80eb0bc2e06d113e908e122c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773565"
---
# <a name="originalvalue-property-ado"></a>Propriedade OriginalValue (ADO)
Indica o valor de um [campo](./field-object.md) que existia no registro antes de qualquer alteração ser feita.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **Variant** que representa o valor de um campo antes de qualquer alteração.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **OriginalValue** para retornar o valor do campo original para um campo do registro atual.  
  
 No *modo de atualização imediata* (no qual o provedor grava alterações na fonte de dados subjacente depois que você chama o método [Update](./update-method.md) ), a propriedade **OriginalValue** retorna o valor do campo que existia antes de qualquer alteração (isto é, desde a última chamada do método **Update** ). Esse é o mesmo valor que o método [CancelUpdate](./cancelupdate-method-ado.md) usa para substituir a propriedade [Value](./value-property-ado.md) .  
  
 No *modo de atualização em lotes* (no qual o provedor armazena em cache várias alterações e as grava na fonte de dados subjacente somente quando você chama o método [UpdateBatch](./updatebatch-method.md) ), a propriedade **OriginalValue** retorna o valor do campo que existia antes de qualquer alteração (ou seja, desde a última chamada do método **UpdateBatch** ). Esse é o mesmo valor que o método [CancelBatch](./cancelbatch-method-ado.md) usa para substituir a propriedade **Value** . Ao usar essa propriedade com a propriedade [subdependent](./underlyingvalue-property.md) , você pode resolver conflitos que surgem de atualizações em lotes.  
  
## <a name="record"></a>Record  
 Para objetos de [registro](./record-object-ado.md) , a propriedade **OriginalValue** estará vazia para os campos adicionados antes de a [atualização](./update-method.md) ser chamada.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](./field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades OriginalValue e subdependvalue (VB)](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Exemplo das propriedades OriginalValue e subdependvalue (VC + +)](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Propriedade UnderlyingValue](./underlyingvalue-property.md)