---
description: Propriedade EOS
title: Propriedade EOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f7df00678197a4b9d16298e5f680263673fd10e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973777"
---
# <a name="eos-property"></a>Propriedade EOS
Indica se a posição atual está no final do [fluxo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor **booliano** que indica se a posição atual está no final do fluxo. **EOS** retornará **true** se não houver mais bytes no fluxo; retornará **false** se houver mais bytes após a posição atual.  
  
 Para definir o fim da posição do fluxo, use o método [SetEOS](../../../ado/reference/ado-api/seteos-method.md) . Para determinar a posição atual, use a propriedade [Position](../../../ado/reference/ado-api/position-property-ado.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades EOS e LineSeparator e do método Skipize (VB)](../../../ado/reference/ado-api/eos-and-lineseparator-properties-and-skipline-method-example-vb.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
