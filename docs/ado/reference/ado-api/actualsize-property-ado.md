---
title: Propriedade ActualSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b864f480542c7ff649bf9b830ba445517dafb91b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698897"
---
# <a name="actualsize-property-ado"></a>Propriedade ActualSize (ADO)
Indica o comprimento real de um valor de campo em bytes.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Retorna um **longo** valor.  
  
## <a name="remarks"></a>Comentários  
 Use o **ActualSize** propriedade para retornar o comprimento real de uma [campo](../../../ado/reference/ado-api/field-object.md) valor do objeto. Todos os campos, o **ActualSize** propriedade é somente leitura. Se o ADO não é possível determinar o comprimento de **campo** valor do objeto, o **ActualSize** propriedade retorna **adUnknown**.  
  
 O **ActualSize** e [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) propriedades são diferentes, conforme mostrado no exemplo a seguir. Um **campo** objeto com um tipo declarado do **adVarChar** e um comprimento máximo de 50 caracteres retorna um **DefinedSize** valor da propriedade de 50, mas o  **Exemplo de ActualSize** é de valor de propriedade que retorna o comprimento dos dados armazenados no campo para o registro atual. **Campos** com um **DefinedSize** maiores que 255 bytes são tratadas como colunas de comprimento variável.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de ActualSize e propriedades DefinedSize (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Exemplo de ActualSize e propriedades DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Propriedade DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)
