---
title: Propriedade ActualSize (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d66019d7a71dd480f1a88a28fe94d72a176497c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="actualsize-property-ado"></a>Propriedade ActualSize (ADO)
Indica o comprimento real de um campo??? valor em bytes.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Retorna um **longo** valor.  
  
## <a name="remarks"></a>Comentários  
 Use o **ActualSize** propriedade para retornar o comprimento real de um [campo](../../../ado/reference/ado-api/field-object.md) valor do objeto. Todos os campos, o **ActualSize** propriedade é somente leitura. Se o ADO não é possível determinar o comprimento de **campo** valor do objeto, o **ActualSize** propriedade retorna **adUnknown**.  
  
 O **ActualSize** e [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) propriedades são diferentes, conforme mostrado no exemplo a seguir. Um **campo** objeto com um tipo declarado de **adVarChar** e um comprimento máximo de 50 caracteres retorna um **DefinedSize** valor da propriedade de 50, mas o ** ActualSize** valor de propriedade retornado é o comprimento dos dados armazenados no campo para o registro atual. **Campos** com um **DefinedSize** maiores que 255 bytes são tratadas como colunas de comprimento variável.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de DefinedSize (VB) e ActualSize](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Exemplo de propriedades de DefinedSize (VC + +) e ActualSize](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propriedade DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)

