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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3970ab8d8f446c4269e4b79c306d2dd9d2cf0426
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762325"
---
# <a name="numericscale-property-ado"></a>Propriedade NumericScale (ADO)
Indica a escala de valores numéricos em um objeto de [campo](../../../ado/reference/ado-api/field-object.md) ou [parâmetro](../../../ado/reference/ado-api/parameter-object.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **byte** que indica o número de casas decimais para as quais os valores numéricos serão resolvidos.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **NumericScale** para determinar quantos dígitos à direita do ponto decimal serão usados para representar valores para um **parâmetro** numérico ou objeto de **campo** .  
  
 Para objetos de **parâmetro** , a propriedade **NumericScale** é leitura/gravação.  
  
 Para um objeto **Field**, **NumericScale** normalmente é somente leitura. No entanto, para novos objetos de **campo** que foram acrescentados à coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** é leitura/gravação somente depois que a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do **campo** tiver sido especificada e o provedor de dados tiver adicionado com êxito o novo **campo** chamando o método [Update](../../../ado/reference/ado-api/update-method.md) da coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Objeto Campo](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades NumericScale e Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Exemplo das propriedades NumericScale e Precision (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Propriedade Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
