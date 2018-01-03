---
title: Propriedade EOS | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EOS
- Stream::EOS
helpviewer_keywords: EOS property
ms.assetid: 57e08c5f-f3ed-4ecd-8c66-50b83b1031d1
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf26c00ecf445c9354d20fa5878942b56f2d2d19
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="eos-property"></a>Propriedade EOS
Indica se a posição atual está no final de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **booliano** valor que indica se a posição atual está no final do fluxo. **EOS** retorna **True** se não houver nenhuma mais bytes no fluxo; ele retorna **False** se não houver mais bytes após a posição atual.  
  
 Para definir o final da posição de fluxo, use o [SetEOS](../../../ado/reference/ado-api/seteos-method.md) método. Para determinar a posição atual, use o [posição](../../../ado/reference/ado-api/position-property-ado.md) propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades de LineSeparator e EOS e exemplo de método SkipLine (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
