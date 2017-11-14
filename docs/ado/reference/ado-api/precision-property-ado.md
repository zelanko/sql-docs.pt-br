---
title: Propriedade Precision (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce6c07fa24f146664ffe5433869e4edf45abdd69
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="precision-property-ado"></a>Propriedade Precision (ADO)
Indica o grau de precisão para valores numéricos em uma [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objeto ou para numérico [campo](../../../ado/reference/ado-api/field-object.md) objetos.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **bytes** valor que indica o número máximo de dígitos usados para representar valores.  
  
## <a name="remarks"></a>Comentários  
 Use o **precisão** propriedade para determinar o número máximo de dígitos usados para representar valores para um numérico **parâmetro** ou **campo** objeto.  
  
 O valor é leitura/gravação em um **parâmetro** objeto.  
  
 Para uma **campo**objeto, **precisão** é normalmente somente leitura. No entanto, para o novo **campo** objetos que foram acrescentados ao [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md), **precisão** é leitura/gravação somente Depois que o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade para o **campo** foi especificado e o provedor de dados foi adicionado com êxito o novo **campo** chamando o [Atualização](../../../ado/reference/ado-api/update-method.md) método o **campos** coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de precisão (VB) e NumericScale](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Exemplo de propriedades de precisão (VC + +) e NumericScale](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Propriedade NumericScale (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)

