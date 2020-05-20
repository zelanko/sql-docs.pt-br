---
title: Propriedade DefinedSize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: rothja
ms.author: jroth
ms.openlocfilehash: 08a7842a2fbfb2bd34f02ad2e45871132111a68f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757392"
---
# <a name="definedsize-property"></a>Propriedade DefinedSize
Indica a capacidade de dados de um objeto de [campo](../../../ado/reference/ado-api/field-object.md) .  
  
## <a name="return-value"></a>Valor Retornado  
 Retorna um valor **longo** que reflete o tamanho definido de um campo, que depende do tipo de dados do objeto Field; consulte [tipo](../../../ado/reference/ado-api/type-property-ado.md) para obter mais informações. Para um campo que usa um tipo de dados de comprimento fixo, o valor de retorno é o tamanho do tipo de dados em bytes. Para um campo que usa um tipo de dados de comprimento variável, este é um dos seguintes:  
  
1.  O comprimento máximo do campo em caracteres (para **adVarChar** e **adVarWChar**) ou em bytes (para **adVarBinary**e **adVarNumeric**) se o campo tiver um comprimento definido. Por exemplo, o campo **adVarChar (5)** tem um comprimento máximo de 5.  
  
2.  O comprimento máximo do tipo de dados em caracteres (para **adChar** e **adWChar**) ou em bytes (para **adBinary** e **adNumeric**) se o campo não tiver um comprimento definido.  
  
3.  ~ 0 (OR bit a bit, o valor não é 0; todos os bits são definidos como 1) se nem o campo nem o tipo de dados têm um comprimento máximo definido.  
  
4.  Para os tipos de dados que não têm um comprimento, isso é definido como ~ 0 (bit que não é o valor 0; todos os bits são definidos como 1).  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **DefinedSize** para determinar a capacidade de dados de um objeto de **campo** .  
  
 As propriedades **DefinedSize** e [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) são diferentes. Por exemplo, considere um objeto **Field** com um tipo declarado de **adVarChar** e um valor de propriedade **DefinedSize** de 50, contendo um único caractere. O valor da propriedade **ActualSize** que ele retorna é o comprimento em bytes do único caractere.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActualSize e DefinedSize (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Exemplo das propriedades ActualSize e DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propriedade ActualSize (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
