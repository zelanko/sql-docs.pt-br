---
title: Propriedade NumericScale (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 39650433fb8b88fb45d38347440d2d612481fb21
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719176"
---
# <a name="numericscale-property-ado"></a>Propriedade NumericScale (ADO)
Indica a escala de valores numéricos em uma [parâmetro](../../../ado/reference/ado-api/parameter-object.md) ou [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **bytes** será possível resolver um valor que indica o número de casas decimais para os quais valores numéricos.  
  
## <a name="remarks"></a>Comentários  
 Use o **NumericScale** propriedade para determinar o número de dígitos à direita do ponto decimal será usado para representar os valores para um numérico **parâmetro** ou **campo** objeto.  
  
 Para **parâmetro** objetos, o **NumericScale** propriedade é leitura/gravação.  
  
 Para um **campo**objeto **NumericScale** é normalmente somente leitura. No entanto, para o novo **campo** objetos que tem sido anexados para o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** é leitura/gravação somente após o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o provedor de dados foi adicionado com êxito o novo **campo** chamando o [ Atualização](../../../ado/reference/ado-api/update-method.md) método da [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Consulte também  
 [NumericScale e exemplo de propriedades Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale e exemplo de propriedades Precision (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Propriedade Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
