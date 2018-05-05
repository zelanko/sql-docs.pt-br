---
title: Propriedade EOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords:
- EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25bab5a0079b07e971200d28bc69e7b36b528523
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="eos-property"></a>Propriedade EOS
Indica se a posição atual está no final de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **booliano** valor que indica se a posição atual está no final do fluxo. **EOS** retorna **True** se não houver nenhuma mais bytes no fluxo; ele retorna **False** se não houver mais bytes após a posição atual.  
  
 Para definir o final da posição de fluxo, use o [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método. Para determinar a posição atual, use o [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de LineSeparator e EOS e exemplo de método SkipLine (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
