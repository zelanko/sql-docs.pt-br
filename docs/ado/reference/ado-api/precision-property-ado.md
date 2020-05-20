---
title: Propriedade Precision (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: rothja
ms.author: jroth
ms.openlocfilehash: f3a72234a6d5e5cbb8e0dc9f5d625b93f15f437f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763327"
---
# <a name="precision-property-ado"></a>Propriedade Precision (ADO)
Indica o grau de precisão para valores numéricos em um objeto de [parâmetro](../../../ado/reference/ado-api/parameter-object.md) ou para objetos de [campo](../../../ado/reference/ado-api/field-object.md) numérico.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **byte** que indica o número máximo de dígitos usados para representar valores.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **precisão** para determinar o número máximo de dígitos usados para representar valores para um **parâmetro** numérico ou objeto de **campo** .  
  
 O valor é leitura/gravação em um objeto de **parâmetro** .  
  
 Para um objeto **Field**, **Precision** normalmente é somente leitura. No entanto, para novos objetos **Field** que foram acrescentados à coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **Precision** é Read/Write only após a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do **campo** ter sido especificada e o provedor de dados adicionou com êxito o novo **campo** chamando o método [Update](../../../ado/reference/ado-api/update-method.md) da coleção **Fields** .  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Campo](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades NumericScale e Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Exemplo das propriedades NumericScale e Precision (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Propriedade NumericScale (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
