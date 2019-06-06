---
title: Propriedade EOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 10b7ee78cb9903ccf0794a197a0679c226141641
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698253"
---
# <a name="eos-property"></a>Propriedade EOS
Indica se a posição atual está no final de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **Boolean** valor que indica se a posição atual está no final do fluxo. **EOS** retorna **verdadeira** se não houver nenhum mais bytes no fluxo; ela retorna **falso** se não houver mais bytes após a posição atual.  
  
 Para definir o final da posição do fluxo, use o [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método. Para determinar a posição atual, use o [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [EOS e LineSeparator propriedades e exemplo de método SkipLine (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
