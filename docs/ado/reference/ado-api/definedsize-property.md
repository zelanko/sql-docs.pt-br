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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4bfb0db701801f1853009594b9d6d24aeb41c629
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933219"
---
# <a name="definedsize-property"></a>Propriedade DefinedSize
Indica a capacidade de dados de um [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **longo** valor que reflete o tamanho definido de um campo, que depende do tipo de dados do objeto field; consulte [tipo](../../../ado/reference/ado-api/type-property-ado.md) para obter mais informações. Para um campo que usa um tipo de dados de comprimento fixo, o valor de retorno é o tamanho do tipo de dados em bytes. Para um campo que usa um tipo de dados de comprimento variável, essa é uma das seguintes opções:  
  
1.  O comprimento máximo do campo em caracteres (para **adVarChar** e **adVarWChar**) ou em bytes (para **adVarBinary**, e **adVarNumeric**) se o campo tem um comprimento definido. Por exemplo, **adVarChar(5)** campo tem um comprimento máximo de 5.  
  
2.  O comprimento máximo do tipo de dados em caracteres (para **adChar** e **adWChar**) ou em bytes (para **adBinary** e **adNumeric**) se a campo não tem um comprimento definido.  
  
3.  ~ 0 (bit a bit, o valor não for 0; todos os bits são definidos como 1) se nem o campo nem o tipo de dados tem um comprimento máximo definido.  
  
4.  Para tipos de dados que não têm um comprimento, isso é definido como ~ 0 (bit a bit, o valor não for 0; todos os bits são definidos como 1).  
  
## <a name="remarks"></a>Comentários  
 Use o **DefinedSize** propriedade para determinar a capacidade de dados de uma **campo** objeto.  
  
 O **DefinedSize** e [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) propriedades são diferentes. Por exemplo, considere uma **campo** objeto com um tipo declarado do **adVarChar** e um **DefinedSize** valor da propriedade de 50, que contém um único caractere. O **ActualSize** é de valor de propriedade que retorna o comprimento em bytes do caractere único.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de ActualSize e propriedades DefinedSize (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Exemplo de ActualSize e propriedades DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propriedade ActualSize (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
