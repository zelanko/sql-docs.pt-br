---
title: Tamanho de propriedade (fluxo de ADO) | Microsoft Docs
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
f1_keywords: _Stream::Size
helpviewer_keywords: Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0a58ee1c4e425af65518a1be5d8629acc849c67
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
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
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Size (Parâmetro ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
