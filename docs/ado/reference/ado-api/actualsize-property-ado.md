---
description: Propriedade ActualSize (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b08a0ce6f9b318430785938c33ce951282eafce2
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88760281"
---
# <a name="actualsize-property-ado"></a>Propriedade ActualSize (ADO)
Indica o comprimento real do valor de um campo em bytes.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Retorna um valor **longo** .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **ActualSize** para retornar o comprimento real do valor de um objeto de [campo](./field-object.md) . Para todos os campos, a propriedade **ActualSize** é somente leitura. Se o ADO não puder determinar o comprimento do valor do objeto **Field** , a propriedade **ActualSize** retornará **adUnknown**.  
  
 As propriedades **ActualSize** e [DefinedSize](./definedsize-property.md) são diferentes, conforme mostrado no exemplo a seguir. Um objeto **Field** com um tipo declarado de **adVarChar** e um comprimento máximo de 50 caracteres retorna um valor de propriedade **DefinedSize** de 50, mas o valor da propriedade **ActualSize** que ele retorna é o comprimento dos dados armazenados no campo para o registro atual. Os **campos** com um **DefinedSize** maior que 255 bytes são tratados como colunas de comprimento variável.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Campo](./field-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActualSize e DefinedSize (VB)](./actualsize-and-definedsize-properties-example-vb.md)   
 [Exemplo das propriedades ActualSize e DefinedSize (VC + +)](./actualsize-and-definedsize-properties-example-vc.md)   
 [Propriedade DefinedSize](./definedsize-property.md)