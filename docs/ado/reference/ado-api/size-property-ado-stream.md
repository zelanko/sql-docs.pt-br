---
title: Tamanho de propriedade (fluxo de ADO) | Microsoft Docs
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
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d60b4fbc39ebe5db98b2185b4d52d7c5c797133
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="size-property-ado-stream"></a>Propriedade Size (fluxo de ADO)
Indica o tamanho do fluxo no número de bytes.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **longo** valor que especifica o tamanho do fluxo no número de bytes. O valor padrão é o tamanho do fluxo ou -1 se o tamanho do fluxo não é conhecido.  
  
## <a name="remarks"></a>Remarks  
 **Tamanho** pode ser usado apenas com open [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
> [!NOTE]
>  Qualquer número de bits pode ser armazenado em uma **fluxo** objeto, limitado apenas pelos recursos do sistema. Se o **fluxo** contém bits maior do que pode ser representado por um **longo** valor, **tamanho** é truncado e, portanto, não representar com exatidão o comprimento do **Fluxo**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Size (Parâmetro ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
