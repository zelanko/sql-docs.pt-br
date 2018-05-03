---
title: Propriedade DefinedSize | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78fe75314e6e2aacf5c6f0d9c599f5cb6db6292
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="definedsize-property"></a>Propriedade DefinedSize
Indica a capacidade de dados de um [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **longo** valor que reflete o tamanho definido de um campo, o que depende do tipo de dados do objeto field; consulte [tipo](../../../ado/reference/ado-api/type-property-ado.md) para obter mais informações. Para um campo que usa um tipo de dados de comprimento fixo, o valor de retorno é o tamanho do tipo de dados em bytes. Para um campo que usa um tipo de dados de comprimento variável, este é um dos seguintes:  
  
1.  O comprimento máximo do campo em caracteres (para **adVarChar** e **adVarWChar**) ou em bytes (para **adVarBinary**, e **adVarNumeric**) se o campo tem um comprimento definido. Por exemplo, **adVarChar(5)** campo tem um comprimento máximo de 5.  
  
2.  O comprimento máximo do tipo de dados em caracteres (para **adChar** e **adWChar**) ou em bytes (para **adBinary** e **adNumeric**) se a campo não tem um comprimento definido.  
  
3.  ~ 0 (bit a bit, o valor não for 0; todos os bits são definidos como 1) se o campo, nem o tipo de dados tem um comprimento máximo definido.  
  
4.  Para tipos de dados que não têm um comprimento, isso é definido como ~ 0 (bit a bit, o valor não for 0; todos os bits são definidos como 1).  
  
## <a name="remarks"></a>Remarks  
 Use o **DefinedSize** propriedade para determinar a capacidade de dados de um **campo** objeto.  
  
 O **DefinedSize** e [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) propriedades são diferentes. Por exemplo, considere um **campo** objeto com um tipo declarado de **adVarChar** e um **DefinedSize** valor da propriedade de 50, que contém um único caractere. O **ActualSize** valor de propriedade retornado é o comprimento em bytes do caractere único.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de DefinedSize (VB) e ActualSize](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Exemplo de propriedades de DefinedSize (VC + +) e ActualSize](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propriedade ActualSize (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
